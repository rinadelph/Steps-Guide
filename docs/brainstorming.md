We are going to build a copy of ebay.com for the venezuelan market. We are going to call it Te Lo Tengo.

We are going to use the following technologies:

- Next.js
- Tailwind CSS
- Shadcn UI
- Clerk
- Lucid
- Lucid Icon
- Supabase
- Vercel

# Product Requirements Document (PRD)

## 1. Project Overview
Te Lo Tengo is an e-commerce marketplace platform specifically designed for the Venezuelan market. The platform will connect Venezuelan buyers and sellers, enabling them to trade new and used items in a secure, user-friendly environment. The name "Te Lo Tengo" (meaning "I've got it for you" in Spanish) emphasizes our focus on local availability and peer-to-peer commerce.

## 2. Core Functionalities

### User Management
- User registration and authentication using Clerk
  - Email and password registration
  - Social login options (Google, Facebook)
  - Phone number verification for Venezuelan users
- User profiles with ratings and reviews
  - Profile picture and basic info
  - Location settings (State/City in Venezuela)
  - Language preference
  - Selling history
  - Buying history
- Seller verification system
  - Venezuelan ID verification
  - Address verification
  - Business registration (optional)
- Multi-language support (Spanish primary, English secondary)

### Product Listings
- Create, edit, and delete product listings
  - Title (max 100 characters)
  - Description (rich text, max 2000 characters)
  - Category selection (max 2 categories)
  - Condition (New, Like New, Good, Fair)
  - Price in USD (auto-conversion to VES)
  - Shipping options
- Product categories and subcategories
  - Maximum 3 levels deep
  - Category-specific attributes
- Multiple product images upload
  - Maximum 8 images per listing
  - Supported formats: JPG, PNG, WEBP
  - Maximum size: 5MB per image
  - Auto-compression and optimization
- Price setting in multiple currencies
  - USD as primary currency
  - VES with daily rate updates
  - Automatic price updates based on exchange rate

### Search and Discovery
- Advanced search functionality with filters
  - Price range
  - Location (by state/city)
  - Condition
  - Seller rating
  - Free shipping options
- Category-based browsing
  - Featured categories on homepage
  - Category-specific landing pages
- Location-based product discovery
  - Default to user's state
  - Radius-based search (km)
- Recently viewed items (last 20 items)

### Buying Process
- Add to cart functionality
  - Maximum 50 items
  - Items grouped by seller
- Watchlist for interested items
  - Maximum 100 items
  - Price change notifications
- Secure checkout process
  - Address validation
  - Multiple shipping options
  - Order summary
- Payment methods
  - Bank transfers (specific Venezuelan banks)
  - Mobile payment apps (Binance, Reserve)
  - International cards
  - Cash on delivery (select locations)

### Selling Tools
- Easy listing creation process
- Inventory management
- Sales analytics dashboard
- Promotion tools for listings
- Bulk listing tools

### Communication
- Built-in messaging system between buyers and sellers
- Automated notifications for orders, messages, and updates
- Dispute resolution system

### Reviews and Ratings
- Product review system
- Seller rating system
- Buyer rating system
- Comment and feedback functionality

### Data Structure
Core Tables Schema:

Products:
- id: uuid
- seller_id: uuid (ref: users)
- title: string
- description: text
- price_usd: decimal
- price_ves: decimal
- condition: enum
- category_id: uuid
- status: enum (active, sold, suspended)
- created_at: timestamp
- updated_at: timestamp

Orders:
- id: uuid
- buyer_id: uuid (ref: users)
- seller_id: uuid (ref: users)
- status: enum (pending, paid, shipped, completed, cancelled)
- total_usd: decimal
- total_ves: decimal
- shipping_address: jsonb
- payment_method: string
- created_at: timestamp

## 3. Technology Stack

### Frontend
- Next.js for the web application framework
- Tailwind CSS for styling
- Shadcn UI for component library
- Lucid and Lucid Icon for iconography

### Backend & Database
- Next.js API routes for backend functionality
- Supabase for database and authentication
- Clerk for user management
- Vercel for hosting and deployment

### Data Structure
- Users table (managed by Clerk)
- Products table
- Categories table
- Orders table
- Reviews table
- Messages table
- Transactions table

### Third-party Integrations
- Payment gateways (specific to Venezuela)
- Image storage (Supabase Storage)
- Email service provider
- SMS verification service
- Maps integration for location-based features

## 4. Security Requirements
- Secure user authentication
- Data encryption
- HTTPS enforcement
- Rate limiting
- Input validation
- XSS protection
- CSRF protection
- Regular security audits

## 5. Performance Requirements
- Page load time under 3 seconds
- Mobile-first responsive design
- Image optimization
- Caching strategies
- API response time under 200ms
- 99.9% uptime

## 6. Future Considerations
- Mobile app development
- Integration with local delivery services
- Advanced analytics dashboard
- AI-powered product recommendations
- Social media integration
- Bulk import/export tools
- International market expansion

## 7. Success Metrics
- User registration and retention rates
- Number of active listings
- Transaction volume
- User satisfaction scores
- Platform uptime
- Response times
- Revenue metrics
