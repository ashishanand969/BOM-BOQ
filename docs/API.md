# 📚 API Documentation - BOM-BOQ Calculator

Complete API documentation for the Bill of Material and Bill of Quantity Calculator.

## Base URL

```
Development: http://localhost:5000
Production: https://api.bom-boq.datoms.io
```

## Authentication

All endpoints (except Auth routes) require a JWT token in the Authorization header.

```bash
Authorization: Bearer <your_jwt_token>
```

### Get JWT Token

1. Register a new user (if first time)
2. Login to receive JWT token
3. Include token in all subsequent requests

## Response Format

All responses follow this format:

```json
{
  "status": "success" | "error",
  "data": {},
  "message": "Optional message",
  "timestamp": "2026-05-30T12:00:00Z"
}
```

## Error Responses

```json
{
  "status": "error",
  "message": "Error description",
  "code": "ERROR_CODE",
  "errors": [
    {
      "field": "fieldName",
      "message": "Field validation error"
    }
  ]
}
```

### Error Codes

| Code | Status | Description |
|------|--------|-------------|
| `INVALID_CREDENTIALS` | 401 | Email or password is incorrect |
| `TOKEN_EXPIRED` | 401 | JWT token has expired |
| `UNAUTHORIZED` | 401 | Missing or invalid token |
| `FORBIDDEN` | 403 | User doesn't have permission |
| `NOT_FOUND` | 404 | Resource not found |
| `VALIDATION_ERROR` | 400 | Input validation failed |
| `DUPLICATE_EMAIL` | 409 | Email already registered |
| `INTERNAL_ERROR` | 500 | Server error |

---

## 🔐 Authentication Endpoints

### Register User

```http
POST /api/auth/register
Content-Type: application/json

{
  "email": "user@datoms.io",
  "password": "SecurePassword123!",
  "name": "John Doe"
}
```

**Response (201):**
```json
{
  "status": "success",
  "data": {
    "id": "user_123",
    "email": "user@datoms.io",
    "name": "John Doe",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expiresIn": 604800
  }
}
```

**Validation Rules:**
- Email must be valid email format
- Email must be unique
- Password must be at least 8 characters
- Password must contain uppercase, lowercase, number, and special character

---

### Login User

```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "user@datoms.io",
  "password": "SecurePassword123!"
}
```

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "id": "user_123",
    "email": "user@datoms.io",
    "name": "John Doe",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expiresIn": 604800
  }
}
```

---

### Logout User

```http
POST /api/auth/logout
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "status": "success",
  "message": "Logged out successfully"
}
```

---

### Refresh Token

```http
POST /api/auth/refresh
Content-Type: application/json

{
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "token": "new_jwt_token",
    "expiresIn": 604800
  }
}
```

---

### Get Current User

```http
GET /api/auth/me
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "id": "user_123",
    "email": "user@datoms.io",
    "name": "John Doe",
    "avatar": "https://...",
    "createdAt": "2026-05-30T10:00:00Z"
  }
}
```

---

## 📁 Project Endpoints

### List User Projects

```http
GET /api/projects
Authorization: Bearer <token>
```

**Query Parameters:**
- `page` (optional, default: 1) - Page number
- `limit` (optional, default: 10) - Items per page
- `sort` (optional) - Sort field (name, createdAt)
- `order` (optional) - Sort order (asc, desc)

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "projects": [
      {
        "id": "proj_123",
        "name": "Project Alpha",
        "description": "First IoT project",
        "createdAt": "2026-05-30T10:00:00Z",
        "updatedAt": "2026-05-30T10:00:00Z",
        "itemCount": {
          "boq": 15,
          "bom": 32
        }
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 10,
      "total": 5,
      "totalPages": 1
    }
  }
}
```

---

### Create Project

```http
POST /api/projects
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "IoT Gateway Project",
  "description": "Smart gateway for IoT devices"
}
```

**Response (201):**
```json
{
  "status": "success",
  "data": {
    "id": "proj_456",
    "name": "IoT Gateway Project",
    "description": "Smart gateway for IoT devices",
    "userId": "user_123",
    "createdAt": "2026-05-30T12:00:00Z",
    "updatedAt": "2026-05-30T12:00:00Z"
  }
}
```

---

### Get Project Details

```http
GET /api/projects/:projectId
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "id": "proj_123",
    "name": "Project Alpha",
    "description": "First IoT project",
    "userId": "user_123",
    "createdAt": "2026-05-30T10:00:00Z",
    "updatedAt": "2026-05-30T10:00:00Z",
    "stats": {
      "boqItems": 15,
      "bomItems": 32,
      "boqTotal": 250000,
      "bomTotal": 150000
    }
  }
}
```

---

### Update Project

```http
PUT /api/projects/:projectId
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "Updated Project Name",
  "description": "Updated description"
}
```

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "id": "proj_123",
    "name": "Updated Project Name",
    "description": "Updated description",
    "updatedAt": "2026-05-30T13:00:00Z"
  }
}
```

---

### Delete Project

```http
DELETE /api/projects/:projectId
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "status": "success",
  "message": "Project deleted successfully"
}
```

---

## 📋 BOQ (Bill of Quantity) Endpoints

### Get BOQ Items

```http
GET /api/projects/:projectId/boq
Authorization: Bearer <token>
```

**Query Parameters:**
- `page` (optional) - Page number
- `limit` (optional) - Items per page
- `sort` (optional) - Sort field

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "items": [
      {
        "id": "boq_123",
        "itemName": "PCB Assembly",
        "description": "Main control board",
        "quantity": 100,
        "unit": "pcs",
        "unitRate": 250.00,
        "gstPercent": 18,
        "subtotal": 25000.00,
        "gstAmount": 4500.00,
        "total": 29500.00,
        "createdAt": "2026-05-30T10:00:00Z"
      }
    ],
    "summary": {
      "totalItems": 1,
      "subtotal": 25000.00,
      "gstAmount": 4500.00,
      "grandTotal": 29500.00
    }
  }
}
```

---

### Create BOQ Item

```http
POST /api/projects/:projectId/boq
Authorization: Bearer <token>
Content-Type: application/json

{
  "itemName": "Microcontroller",
  "description": "ESP32 Development Board",
  "quantity": 50,
  "unit": "pcs",
  "unitRate": 400.00,
  "gstPercent": 18
}
```

**Response (201):**
```json
{
  "status": "success",
  "data": {
    "id": "boq_456",
    "itemName": "Microcontroller",
    "description": "ESP32 Development Board",
    "quantity": 50,
    "unit": "pcs",
    "unitRate": 400.00,
    "gstPercent": 18,
    "subtotal": 20000.00,
    "gstAmount": 3600.00,
    "total": 23600.00,
    "createdAt": "2026-05-30T12:00:00Z"
  }
}
```

**Validation:**
- itemName: Required, max 255 characters
- quantity: Required, > 0
- unitRate: Required, > 0
- gstPercent: Optional, 0-100

---

### Update BOQ Item

```http
PUT /api/projects/:projectId/boq/:itemId
Authorization: Bearer <token>
Content-Type: application/json

{
  "quantity": 75,
  "unitRate": 450.00,
  "gstPercent": 18
}
```

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "id": "boq_456",
    "itemName": "Microcontroller",
    "quantity": 75,
    "unitRate": 450.00,
    "gstPercent": 18,
    "subtotal": 33750.00,
    "gstAmount": 6075.00,
    "total": 39825.00,
    "updatedAt": "2026-05-30T13:00:00Z"
  }
}
```

---

### Delete BOQ Item

```http
DELETE /api/projects/:projectId/boq/:itemId
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "status": "success",
  "message": "BOQ item deleted successfully"
}
```

---

### Export BOQ

```http
POST /api/projects/:projectId/boq/export
Authorization: Bearer <token>
Content-Type: application/json

{
  "format": "excel",
  "includeGST": true,
  "fileName": "BOQ_Report"
}
```

**Supported Formats:**
- `excel` - Microsoft Excel (.xlsx)
- `pdf` - PDF Document (.pdf)
- `csv` - CSV Format (.csv)
- `json` - JSON Format (.json)

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "downloadUrl": "/api/downloads/boq_export_xyz.xlsx",
    "fileName": "BOQ_Report.xlsx",
    "format": "excel",
    "size": 15234,
    "createdAt": "2026-05-30T13:00:00Z"
  }
}
```

---

## 📦 BOM (Bill of Material) Endpoints

### Get BOM Items

```http
GET /api/projects/:projectId/bom
Authorization: Bearer <token>
```

**Query Parameters:**
- `page` (optional) - Page number
- `limit` (optional) - Items per page
- `category` (optional) - Filter by category
- `hierarchy` (optional, boolean) - Return hierarchical structure

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "items": [
      {
        "id": "bom_123",
        "componentName": "LED Module",
        "description": "RGB LED Array",
        "quantity": 200,
        "costPerUnit": 15.50,
        "supplier": "ElectroSmart Ltd",
        "category": "LEDs",
        "total": 3100.00,
        "createdAt": "2026-05-30T10:00:00Z"
      }
    ],
    "summary": {
      "totalItems": 1,
      "totalCost": 3100.00,
      "totalQuantity": 200,
      "categories": ["LEDs"]
    }
  }
}
```

---

### Create BOM Item

```http
POST /api/projects/:projectId/bom
Authorization: Bearer <token>
Content-Type: application/json

{
  "componentName": "Temperature Sensor",
  "description": "DHT22 Temperature & Humidity Sensor",
  "quantity": 100,
  "costPerUnit": 8.99,
  "supplier": "SensorCorp Inc",
  "category": "Sensors"
}
```

**Response (201):**
```json
{
  "status": "success",
  "data": {
    "id": "bom_456",
    "componentName": "Temperature Sensor",
    "description": "DHT22 Temperature & Humidity Sensor",
    "quantity": 100,
    "costPerUnit": 8.99,
    "supplier": "SensorCorp Inc",
    "category": "Sensors",
    "total": 899.00,
    "createdAt": "2026-05-30T12:00:00Z"
  }
}
```

---

### Update BOM Item

```http
PUT /api/projects/:projectId/bom/:itemId
Authorization: Bearer <token>
Content-Type: application/json

{
  "quantity": 150,
  "costPerUnit": 8.50,
  "supplier": "NewSupplier Corp"
}
```

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "id": "bom_456",
    "componentName": "Temperature Sensor",
    "quantity": 150,
    "costPerUnit": 8.50,
    "supplier": "NewSupplier Corp",
    "total": 1275.00,
    "updatedAt": "2026-05-30T13:00:00Z"
  }
}
```

---

### Delete BOM Item

```http
DELETE /api/projects/:projectId/bom/:itemId
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "status": "success",
  "message": "BOM item deleted successfully"
}
```

---

### Export BOM

```http
POST /api/projects/:projectId/bom/export
Authorization: Bearer <token>
Content-Type: application/json

{
  "format": "excel",
  "includeSuppliers": true,
  "fileName": "BOM_Report"
}
```

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "downloadUrl": "/api/downloads/bom_export_xyz.xlsx",
    "fileName": "BOM_Report.xlsx",
    "format": "excel",
    "size": 12456,
    "createdAt": "2026-05-30T13:00:00Z"
  }
}
```

---

## Rate Limiting

API endpoints are rate limited to prevent abuse:

- **Standard Endpoints:** 100 requests per 15 minutes
- **Auth Endpoints:** 5 requests per 15 minutes
- **Export Endpoints:** 10 requests per 15 minutes

When rate limit is exceeded, you'll receive:

```json
{
  "status": "error",
  "code": "RATE_LIMIT_EXCEEDED",
  "message": "Too many requests, please try again later",
  "retryAfter": 300
}
```

---

## Example Usage with cURL

### Register and Login

```bash
# Register
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@datoms.io",
    "password": "SecurePassword123!",
    "name": "John Doe"
  }'

# Save the token from response

# Login
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@datoms.io",
    "password": "SecurePassword123!"
  }'
```

### Create Project

```bash
TOKEN="your_jwt_token_here"

curl -X POST http://localhost:5000/api/projects \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "My First Project",
    "description": "Testing BOM-BOQ calculator"
  }'
```

### Add BOQ Item

```bash
TOKEN="your_jwt_token_here"
PROJECT_ID="proj_123"

curl -X POST http://localhost:5000/api/projects/$PROJECT_ID/boq \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "itemName": "Component A",
    "description": "Main component",
    "quantity": 100,
    "unit": "pcs",
    "unitRate": 250.00,
    "gstPercent": 18
  }'
```

---

## Webhook Support (Coming Soon)

Webhooks will allow you to receive notifications for:
- Project updates
- Item additions/modifications
- Export completions
- User actions

---

## API Version

Current API Version: **v1.0.0**

---

**For more information, visit [GitHub](https://github.com/ashishanand969/BOM-BOQ) or contact support@datoms.io**
