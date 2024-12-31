# Project File Structure

📁 te-lo-tengo/
├── 📁 app/                      # Next.js app router pages
│   ├── 📁 (auth)/              # Auth-related routes
│   │   ├── login/
│   │   │   ├── page.tsx
│   │   │   ├── loading.tsx
│   │   │   └── error.tsx
│   │   ├── verify/
│   │   │   ├── page.tsx
│   │   │   ├── loading.tsx
│   │   │   └── error.tsx
│   │   └── profile/
│   │       ├── page.tsx
│   │       ├── edit/
│   │       │   └── page.tsx
│   │       └── settings/
│   │           └── page.tsx
│   ├── 📁 (marketplace)/       # Main marketplace features
│   │   ├── products/
│   │   │   ├── page.tsx        # Products listing
│   │   │   ├── [id]/           # Individual product
│   │   │   │   ├── page.tsx
│   │   │   │   ├── edit/
│   │   │   │   └── delete/
│   │   │   ├── new/           # Create listing
│   │   │   │   ├── page.tsx
│   │   │   │   └── preview/
│   │   │   └── my-listings/   # User's listings
│   │   ├── categories/
│   │   │   ├── page.tsx
│   │   │   └── [category]/
│   │   │       └── page.tsx
│   │   └── search/
│   │       ├── page.tsx
│   │       └── filters/
│   ├── 📁 (chat)/              # Chat system routes
│   │   ├── inbox/
│   │   │   ├── page.tsx
│   │   │   └── archived/
│   │   └── [conversationId]/
│   │       ├── page.tsx
│   │       └── media/
│   ├── 📁 (cart)/             # Shopping cart
│   │   ├── page.tsx
│   │   └── checkout/
│   │       ├── page.tsx
│   │       ├── shipping/
│   │       ├── payment/
│   │       └── confirmation/
│   ├── 📁 (account)/          # User account
│   │   ├── dashboard/
│   │   ├── orders/
│   │   ├── wishlist/
│   │   └── settings/
│   └── 📁 api/                 # API routes
│       ├── auth/
│       ├── products/
│       ├── chat/
│       ├── payments/
│       └── webhooks/
│
├── 📁 components/              # React components
│   ├── 📁 auth/               # Auth-related components
│   ├── 📁 products/           # Product-related components
│   ├── 📁 chat/               # Chat components
│   ├── 📁 ui/                 # Reusable UI components
│   └── 📁 shared/             # Shared components
│
├── 📁 lib/                    # Core functionality
│   ├── 📁 auth/               # Auth utilities & services
│   │   ├── whatsapp.ts       # WhatsApp integration
│   │   └── telegram.ts       # Telegram bot integration
│   ├── 📁 db/                # Database utilities
│   ├── 📁 api/               # API utilities
│   ├── 📁 utils/             # Helper functions
│   ├── 📁 cache/           # Caching strategies
│   │   ├── redis.ts       # Redis configuration
│   │   └── memory.ts      # In-memory caching
│   ├── 📁 monitoring/     # Performance monitoring
│   │   ├── metrics.ts    # Metrics collection
│   │   └── logging.ts    # Logging configuration
│   └── 📁 monitoring/     # Performance monitoring
│       ├── metrics.ts    # Metrics collection
│       └── logging.ts    # Logging configuration
│
├── 📁 services/               # External service integrations
│   ├── 📁 payments/          # Payment integrations
│   ├── 📁 storage/           # Storage services
│   ├── 📁 messaging/         # Messaging services
│   └── 📁 queue/          # Background job processing
│       ├── 📁 jobs/         # Job definitions
│       └── 📁 workers/      # Job workers
│
├── 📁 config/                # Configuration files
│   ├── site.ts              # Site configuration
│   └── constants.ts         # Constants
│
├── 📁 types/                 # TypeScript type definitions
│   ├── auth.ts
│   ├── products.ts
│   └── api.ts
│
├── 📁 styles/                # Global styles
│   └── globals.css
│
├── 📁 public/                # Static files
│   ├── 📁 images/
│   └── 📁 icons/
│
├── 📁 scripts/               # Utility scripts
│   ├── seed.ts
│   └── migrations/
│
├── 📁 docs/                  # Documentation
│   ├── setup.md
│   ├── architecture.md
│   └── api.md
│
├── 📁 tests/                 # Test files
│   ├── 📁 unit/
│   ├── 📁 integration/
│   └── 📁 e2e/
│
├── .env.example             # Environment variables example
├── .env.local              # Local environment variables
├── package.json
└── README.md 