---
title: "API Reference"
description: "Complete API documentation and examples"
category: "Reference"
category_icon: "📖"
category_description: "Technical reference documentation."
order: 1
last_updated: "2024-01-01"
toc: true
tags: [api, reference, endpoints]
related:
  - Configuration
  - Getting Started
---

## Overview

The REST API follows standard HTTP conventions. All requests and responses use JSON.

**Base URL:** `https://your-domain.com/api/v1`

**Authentication:** Include your token in the `Authorization` header:
```
Authorization: Bearer YOUR_TOKEN
```

## Authentication

### POST /auth/token

Obtain an access token.

**Request Body:**
```json
{
  "username": "your-username",
  "password": "your-password"
}
```

**Response:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9...",
  "expires_at": "2024-12-31T23:59:59Z"
}
```

## Resources

### Items

#### GET /items

List all items.

**Query Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `page` | integer | Page number (default: 1) |
| `per_page` | integer | Items per page (default: 20, max: 100) |
| `sort` | string | Sort field: `created_at`, `name` |
| `order` | string | Sort order: `asc`, `desc` |
| `filter` | string | Filter query |

**Example Request:**
```bash
curl -H "Authorization: Bearer TOKEN" \
  "https://your-domain.com/api/v1/items?page=1&per_page=10"
```

**Example Response:**
```json
{
  "data": [
    {
      "id": "item_123",
      "name": "Example Item",
      "status": "active",
      "created_at": "2024-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "per_page": 10,
    "total": 42,
    "total_pages": 5
  }
}
```

#### GET /items/:id

Get a specific item by ID.

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | string | Item ID |

**Example Response:**
```json
{
  "id": "item_123",
  "name": "Example Item",
  "description": "A detailed description",
  "status": "active",
  "metadata": {
    "key": "value"
  },
  "created_at": "2024-01-15T10:30:00Z",
  "updated_at": "2024-01-20T14:22:00Z"
}
```

#### POST /items

Create a new item.

**Request Body:**
```json
{
  "name": "New Item",
  "description": "Item description",
  "metadata": {
    "custom_key": "custom_value"
  }
}
```

**Response:** `201 Created`
```json
{
  "id": "item_456",
  "name": "New Item",
  "status": "active",
  "created_at": "2024-01-21T09:00:00Z"
}
```

#### PUT /items/:id

Update an existing item.

**Request Body:** Same as POST (all fields optional).

**Response:** `200 OK` with updated item.

#### DELETE /items/:id

Delete an item.

**Response:** `204 No Content`

## Error Handling

All errors follow this format:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {}
  }
}
```

### HTTP Status Codes

| Code | Meaning |
|------|---------|
| `200` | OK |
| `201` | Created |
| `204` | No Content |
| `400` | Bad Request — Invalid input |
| `401` | Unauthorized — Invalid or missing token |
| `403` | Forbidden — Insufficient permissions |
| `404` | Not Found |
| `429` | Too Many Requests — Rate limited |
| `500` | Internal Server Error |

### Error Codes

| Code | Description |
|------|-------------|
| `INVALID_INPUT` | Request body validation failed |
| `NOT_FOUND` | Resource not found |
| `UNAUTHORIZED` | Authentication required |
| `RATE_LIMITED` | Too many requests |

## Rate Limiting

API requests are rate limited:

- **Authenticated:** 1000 requests per hour
- **Unauthenticated:** 60 requests per hour

Rate limit headers are included in every response:

```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 998
X-RateLimit-Reset: 1706518800
```

## SDKs & Client Libraries

Official client libraries:

- **JavaScript/Node.js:** `npm install your-sdk`
- **Python:** `pip install your-sdk`
- **Go:** `go get github.com/your-org/your-sdk-go`

### JavaScript Example

```javascript
const { Client } = require('your-sdk');

const client = new Client({
  token: process.env.YOUR_TOOL_TOKEN
});

// List items
const items = await client.items.list({ per_page: 10 });

// Create item
const newItem = await client.items.create({
  name: 'My Item',
  description: 'Created via SDK'
});
```
