# API Documentation

## Overview
Te Lo Tengo's API is built using Next.js API routes with TypeScript. All endpoints follow RESTful conventions and return JSON responses.

## Base URL
```
Production: https://telotengo.com/api
Development: http://localhost:3000/api
```

## Authentication
All authenticated endpoints require a Bearer token in the Authorization header:
```
Authorization: Bearer <token>
```

## Response Format
All responses follow this structure:
```typescript
{
  success: boolean;
  data?: any;
  error?: {
    code: string;
    message: string;
    details?: any;
  };
}
```

## Error Codes
- `AUTH_REQUIRED`: Authentication required
- `INVALID_TOKEN`: Invalid or expired token
- `NOT_FOUND`: Resource not found
- `VALIDATION_ERROR`: Invalid input data
- `FORBIDDEN`: Insufficient permissions
- `INTERNAL_ERROR`: Server error

## Rate Limiting
- 100 requests per minute for authenticated users
- 20 requests per minute for unauthenticated users

## Endpoints

### Products

#### GET /api/products
List all products with pagination.

Query Parameters:
- `page` (optional): Page number (default: 1)
- `limit` (optional): Items per page (default: 20)
- `category` (optional): Filter by category
- `search` (optional): Search term
- `sort` (optional): Sort field (price, date, rating)
- `order` (optional): Sort order (asc, desc)

Response:
```typescript
{
  success: true,
  data: {
    items: Array<{
      id: string;
      title: string;
      description: string;
      price: number;
      images: string[];
      category: string;
      seller: {
        id: string;
        name: string;
        rating: number;
      };
      createdAt: string;
      updatedAt: string;
    }>;
    pagination: {
      page: number;
      limit: number;
      total: number;
      pages: number;
    };
  }
}
```

#### POST /api/products
Create a new product. Requires authentication.

Request Body:
```typescript
{
  title: string;
  description: string;
  price: number;
  images: string[];
  category: string;
}
```

### Users

#### GET /api/users/me
Get current user profile. Requires authentication.

Response:
```typescript
{
  success: true,
  data: {
    id: string;
    name: string;
    email: string;
    role: string;
    createdAt: string;
    updatedAt: string;
  }
}
```

### Orders

#### POST /api/orders
Create a new order. Requires authentication.

Request Body:
```typescript
{
  items: Array<{
    productId: string;
    quantity: number;
  }>;
  shippingAddress: {
    street: string;
    city: string;
    state: string;
    zipCode: string;
  };
}
```

## WebSocket Events
Real-time updates are available through WebSocket connections.

### Chat Messages
```typescript
// Subscribe to chat messages
socket.on('chat:message', (data: {
  id: string;
  senderId: string;
  receiverId: string;
  content: string;
  timestamp: string;
}) => void);

// Send a chat message
socket.emit('chat:send', {
  receiverId: string;
  content: string;
});
```

### Order Updates
```typescript
// Subscribe to order status updates
socket.on('order:update', (data: {
  orderId: string;
  status: 'pending' | 'processing' | 'shipped' | 'delivered';
  timestamp: string;
}) => void);
```

## Development Guidelines
1. All endpoints must validate input data using Zod schemas
2. Use appropriate HTTP status codes
3. Include rate limiting headers in responses
4. Log all errors with appropriate context
5. Document all changes in OpenAPI specification 