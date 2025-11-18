# AgriSmart API Endpoints

Base URL: `http://localhost:5000`

## Authentication Endpoints

### Clerk Sync (NEW - Primary Authentication)
```
POST /api/auth/clerk-sync
```
**Description**: Sync Clerk user to MongoDB after authentication  
**Body**:
```json
{
  "clerkId": "user_xxxxx",
  "email": "user@example.com",
  "name": "John Doe",
  "role": "farmer" | "buyer" | "admin",
  "phone": "+1234567890",
  "location": "California"
}
```
**Response**:
```json
{
  "message": "User created successfully",
  "user": {
    "_id": "...",
    "clerkId": "user_xxxxx",
    "email": "user@example.com",
    "name": "John Doe",
    "role": "farmer",
    "phone": "+1234567890",
    "location": "California",
    "approved": true,
    "createdAt": "2024-01-01T00:00:00.000Z"
  }
}
```

---

### Get User by Clerk ID (NEW)
```
GET /api/auth/clerk-user/:clerkId
```
**Description**: Fetch user data using Clerk ID  
**Response**:
```json
{
  "user": {
    "_id": "...",
    "clerkId": "user_xxxxx",
    "email": "user@example.com",
    "name": "John Doe",
    "role": "farmer",
    "approved": true
  }
}
```

---

### Register (Legacy - For Backward Compatibility)
```
POST /api/auth/register
```
**Description**: Register a new user with password  
**Body**:
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123",
  "role": "farmer",
  "phone": "+1234567890",
  "location": "California"
}
```
**Response**:
```json
{
  "message": "User registered successfully",
  "user": { ... },
  "token": "jwt_token_here"
}
```

---

### Login (Legacy - For Backward Compatibility)
```
POST /api/auth/login
```
**Description**: Login with email and password  
**Body**:
```json
{
  "email": "john@example.com",
  "password": "password123"
}
```
**Response**:
```json
{
  "message": "Login successful",
  "user": { ... },
  "token": "jwt_token_here"
}
```

---

### Get Current User
```
GET /api/auth/me
Headers: Authorization: Bearer {token}
```
**Description**: Get currently logged-in user's data  

---

## Product Endpoints

### Get All Products
```
GET /api/products
```
**Description**: Fetch all approved products  

---

### Get My Products (Farmer Only)
```
GET /api/products/my-products
Headers: Authorization: Bearer {token}
```
**Description**: Fetch products belonging to the logged-in farmer  

---

### Create Product (Farmer Only)
```
POST /api/products
Headers: Authorization: Bearer {token}
```
**Body**:
```json
{
  "name": "Fresh Tomatoes",
  "category": "Vegetables",
  "price": 5.99,
  "quantity": 100,
  "unit": "kg",
  "description": "Organic tomatoes fresh from the farm",
  "image": "https://example.com/tomato.jpg"
}
```

---

### Update Product (Farmer Only)
```
PUT /api/products/:id
Headers: Authorization: Bearer {token}
```
**Body**: Same as create product  

---

### Delete Product (Farmer Only)
```
DELETE /api/products/:id
Headers: Authorization: Bearer {token}
```

---

## Message Endpoints

### Send Message (Buyer to Farmer)
```
POST /api/messages
Headers: Authorization: Bearer {token}
```
**Body**:
```json
{
  "farmerId": "farmer_id_here",
  "productId": "product_id_here",
  "message": "I'm interested in buying your tomatoes"
}
```

---

### Get Messages (Farmer)
```
GET /api/messages/farmer
Headers: Authorization: Bearer {token}
```
**Description**: Fetch all messages sent to the logged-in farmer  

---

### Get Messages (Buyer)
```
GET /api/messages/buyer
Headers: Authorization: Bearer {token}
```
**Description**: Fetch all messages sent by the logged-in buyer  

---

## Admin Endpoints

### Get All Users (Admin Only)
```
GET /api/admin/users
Headers: Authorization: Bearer {token}
```
**Description**: Fetch all users in the system  

---

### Approve User (Admin Only)
```
PATCH /api/admin/users/:id/approve
Headers: Authorization: Bearer {token}
```
**Description**: Approve a pending user (mainly for legacy users)  

---

### Delete User (Admin Only)
```
DELETE /api/admin/users/:id
Headers: Authorization: Bearer {token}
```
**Description**: Delete a user from the system  

---

### Get All Products (Admin Only)
```
GET /api/admin/products
Headers: Authorization: Bearer {token}
```
**Description**: Fetch all products (approved and pending)  

---

### Delete Product (Admin Only)
```
DELETE /api/admin/products/:id
Headers: Authorization: Bearer {token}
```
**Description**: Delete any product from the system  

---

## Response Codes

- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `500` - Server Error

## Authentication Flow with Clerk

1. User signs up/signs in via Clerk on frontend
2. Frontend receives Clerk user object with `clerkId`
3. User completes role selection (if new user)
4. Frontend calls `POST /api/auth/clerk-sync` with user details
5. Backend creates/updates user in MongoDB
6. User data is stored in localStorage for quick access
7. Future API calls can use Clerk ID to identify user

## Notes

- **Clerk Users**: No admin approval needed, `approved` is always `true`
- **Legacy Users**: Created via register endpoint, may need approval
- **Authorization**: Some endpoints require JWT token in Authorization header
- **CORS**: Enabled for frontend at `http://localhost:3000` (or your dev port)
- **Demo Mode**: Frontend works without backend connection using mock data
