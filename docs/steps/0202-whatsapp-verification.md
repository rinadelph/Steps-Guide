# Step 0202: WhatsApp Verification Implementation

## Overview
This document outlines the implementation of phone number verification using WhatsApp Business API. This method provides a familiar and reliable verification experience for Venezuelan users.

## Prerequisites
1. Set up WhatsApp Business API:
   - Create Meta Business Account
   - Set up WhatsApp Business API through Meta or a provider (e.g., Twilio)
   - Get verified business account
   - Complete business verification process
   - Get API credentials

2. Set up environment variables:
   ```env
   WHATSAPP_API_KEY=your_api_key
   WHATSAPP_BUSINESS_ACCOUNT_ID=your_account_id
   WHATSAPP_PHONE_NUMBER_ID=your_phone_number_id
   ```

## Implementation Steps

### 1. Create WhatsApp Service
1. Create a new service to handle WhatsApp API interactions
2. Implement methods for:
   - Sending verification codes
   - Managing message templates
   - Handling API responses
   - Error handling and retries

### 2. Database Schema Updates
1. Add verification_attempts table (if not already created for Telegram):
   ```sql
   CREATE TABLE verification_attempts (
     id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
     phone_number VARCHAR NOT NULL,
     verification_code VARCHAR NOT NULL,
     attempts INTEGER DEFAULT 0,
     verified BOOLEAN DEFAULT FALSE,
     verification_method VARCHAR NOT NULL, -- 'whatsapp' or 'telegram'
     expires_at TIMESTAMP WITH TIME ZONE NOT NULL,
     created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
     updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
   );

   -- Add indexes
   CREATE INDEX idx_verification_phone ON verification_attempts(phone_number);
   CREATE INDEX idx_verification_expires ON verification_attempts(expires_at);
   CREATE INDEX idx_verification_method ON verification_attempts(verification_method);
   ```

### 3. API Endpoints
1. Create endpoint for initiating verification:
   ```typescript
   POST /api/auth/whatsapp/verify
   Body: { phone_number: string }
   ```

2. Create endpoint for validating code:
   ```typescript
   POST /api/auth/whatsapp/validate
   Body: { phone_number: string, code: string }
   ```

### 4. WhatsApp Message Templates
1. Create and get approval for message templates:
   - Verification code template
   - Welcome message template
   - Success confirmation template

2. Template example:
   ```
   Verification Code Template:
   Name: verification_code
   Language: es
   Category: AUTHENTICATION
   Content: Tu código de verificación para Te Lo Tengo es {{1}}. Este código expira en 10 minutos.
   ```

### 5. Verification Flow
1. User enters phone number in the UI
2. Backend:
   - Validates phone number format
   - Generates verification code
   - Creates verification attempt record
   - Sends WhatsApp message using template
3. User receives WhatsApp message
4. User enters code in verification page
5. Backend validates and completes verification

### 6. Security Measures
1. Rate limiting:
   - Maximum 3 attempts per code
   - Maximum 5 verification attempts per phone number per day
   - 5-minute cooldown between sending new codes

2. Code expiration:
   - Verification codes expire after 10 minutes
   - Expired codes are automatically invalidated

3. Phone number validation:
   - Validate format (+58 required for Venezuela)
   - Check for WhatsApp registration
   - Block known spam numbers

### 7. Error Handling
1. Handle WhatsApp API specific errors:
   - Template errors
   - Rate limits
   - Invalid numbers
   - Network issues
   - Account status issues

2. Implement fallback mechanisms:
   - Retry logic for failed messages
   - Option to switch to Telegram verification
   - Clear error messages for users

### 8. User Experience
1. Clear instructions:
   - What WhatsApp number will message them
   - What message to expect
   - How to verify it's official

2. Status indicators:
   - Message sent
   - Message delivered
   - Message read
   - Verification success/failure

### 9. Monitoring and Analytics
1. Track metrics:
   - Message delivery rates
   - Verification success rates
   - Error rates
   - Average verification time

2. Set up alerts for:
   - High failure rates
   - API quota limits
   - Account status changes

## Technical Details

### WhatsApp API Integration
```typescript
interface WhatsAppConfig {
  apiVersion: string;
  accountId: string;
  phoneNumberId: string;
  apiKey: string;
  templates: {
    verificationCode: string;
    welcome: string;
    success: string;
  };
}
```

### Message Templates
1. Verification Code Message:
```
🔐 Código de Verificación Te Lo Tengo

Tu código es: {{code}}

⚠️ Este código expira en 10 minutos.
❌ No compartas este código con nadie.
```

2. Welcome Message:
```
👋 ¡Bienvenido a Te Lo Tengo!

Gracias por elegir nuestra plataforma. Estamos verificando tu número para brindarte una experiencia segura.
```

### Error Handling Strategy
```typescript
interface WhatsAppError {
  code: string;
  message: string;
  retryable: boolean;
  action: 'retry' | 'fallback' | 'fail';
}

const errorStrategies: Record<string, WhatsAppError> = {
  'rate_limit': {
    code: 'RATE_LIMIT',
    message: 'Has excedido el límite de intentos',
    retryable: true,
    action: 'retry'
  },
  'invalid_number': {
    code: 'INVALID_NUMBER',
    message: 'Número no válido para WhatsApp',
    retryable: false,
    action: 'fallback'
  }
  // ... more error strategies
};
```

## Next Steps
1. Set up WhatsApp Business API account
2. Create and get approval for message templates
3. Implement WhatsApp service
4. Set up monitoring and analytics
5. Create test suite
6. Document API endpoints
7. Implement fallback mechanisms

## Cost Considerations
1. WhatsApp Business API costs:
   - Template message costs
   - Session message costs
   - Business verification costs

2. Cost optimization:
   - Use session messages when possible
   - Implement proper error handling to avoid unnecessary retries
   - Monitor usage and adjust limits accordingly 