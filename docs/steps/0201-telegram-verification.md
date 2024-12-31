# Step 0201: Telegram Verification Implementation

## Overview
This document outlines the implementation of phone number verification using Telegram's Bot API. This method is cost-effective and reliable for the Venezuelan market.

## Prerequisites
1. Create a Telegram Bot:
   - Talk to [@BotFather](https://t.me/botfather) on Telegram
   - Use the `/newbot` command
   - Choose a name and username for the bot
   - Save the bot token provided by BotFather

2. Set up environment variables:
   ```env
   TELEGRAM_BOT_TOKEN=your_bot_token
   TELEGRAM_BOT_USERNAME=your_bot_username
   ```

## Implementation Steps

### 1. Create Telegram Bot Service
1. Create a new service to handle Telegram bot interactions
2. Implement methods for:
   - Sending verification codes
   - Validating received codes
   - Managing verification attempts

### 2. Database Schema Updates
1. Add verification_attempts table:
   ```sql
   CREATE TABLE verification_attempts (
     id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
     phone_number VARCHAR NOT NULL,
     verification_code VARCHAR NOT NULL,
     attempts INTEGER DEFAULT 0,
     verified BOOLEAN DEFAULT FALSE,
     expires_at TIMESTAMP WITH TIME ZONE NOT NULL,
     created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
     updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
   );

   -- Add indexes
   CREATE INDEX idx_verification_phone ON verification_attempts(phone_number);
   CREATE INDEX idx_verification_expires ON verification_attempts(expires_at);
   ```

### 3. API Endpoints
1. Create endpoint for initiating verification:
   ```typescript
   POST /api/auth/telegram/verify
   Body: { phone_number: string }
   ```

2. Create endpoint for validating code:
   ```typescript
   POST /api/auth/telegram/validate
   Body: { phone_number: string, code: string }
   ```

### 4. Verification Flow
1. User enters phone number in the UI
2. Backend generates a 6-digit code
3. Bot sends message to user with:
   - Verification code
   - Instructions to enter code on website
   - Link to return to website
4. User enters code in verification page
5. Backend validates code and creates/updates user account

### 5. Security Measures
1. Rate limiting:
   - Maximum 3 attempts per code
   - Maximum 5 verification attempts per phone number per day
   - 5-minute cooldown between sending new codes

2. Code expiration:
   - Verification codes expire after 10 minutes
   - Expired codes are automatically invalidated

3. Phone number validation:
   - Validate format (+58 required for Venezuela)
   - Check for suspicious patterns
   - Block known spam numbers

### 6. Error Handling
1. Implement proper error messages for:
   - Invalid phone numbers
   - Rate limit exceeded
   - Invalid/expired codes
   - Network issues
   - Bot API errors

### 7. User Experience
1. Show clear instructions:
   - How to find the bot on Telegram
   - What message to expect
   - Where to enter the code

2. Provide helpful error messages:
   - When verification fails
   - When rate limits are hit
   - When code expires

### 8. Testing
1. Test cases to implement:
   - Successful verification flow
   - Invalid code attempts
   - Rate limiting
   - Code expiration
   - Network error handling
   - Bot API error handling

## Technical Details

### Telegram Bot Commands
```
/start - Initialize bot and get instructions
/help - Get help with verification process
/cancel - Cancel current verification attempt
```

### Message Templates
1. Verification Code Message:
```
🔐 Código de Verificación Te Lo Tengo

Tu código es: {code}

⚠️ Este código expira en 10 minutos.
❌ No compartas este código con nadie.
✅ Regresa a la página web para completar tu verificación.
```

2. Success Message:
```
✅ ¡Verificación exitosa!

Puedes cerrar esta conversación y continuar en la página web.
```

### Rate Limiting Implementation
```typescript
interface RateLimitConfig {
  maxAttempts: number;        // 3 attempts per code
  maxDailyAttempts: number;   // 5 attempts per day
  cooldownPeriod: number;     // 5 minutes
  codeExpiration: number;     // 10 minutes
}
```

## Next Steps
1. Implement Telegram bot service
2. Create database migrations
3. Set up API endpoints
4. Implement rate limiting
5. Add error handling
6. Create test suite
7. Document API endpoints 