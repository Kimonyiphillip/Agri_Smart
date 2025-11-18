# AgriSmart Backend API

Backend server for AgriSmart Farm Produce Marketplace built with Node.js, Express, and MongoDB.

## 🚀 Quick Start

### Prerequisites

- Node.js (v14 or higher)
- MongoDB (local or MongoDB Atlas)
- npm or yarn

### Installation

1. **Navigate to backend directory:**

```bash
cd backend
```

2. **Install dependencies:**

```bash
npm install
```

3. **Setup environment variables:**

```bash
# Copy the example env file
cp .env.example .env

# Edit .env and add your configurations
# Make sure to set:
# - MONGODB_URI (your MongoDB connection string)
# - JWT_SECRET (a secure random string)
```

4. **Start MongoDB:**

```bash
# If using local MongoDB
mongod

# If using MongoDB Atlas, just use the connection string in .env
```

5. **Run the server:**

```bash
# Development mode with auto-reload
npm run dev

# Production mode
npm start
```

The server will run on `http://localhost:5000`

## 📁 Project Structure

```
backend/
├── models/
│   ├── User.js          # User schema (Farmer, Buyer, Admin)
│   ├── Product.js       # Product schema
│   └── Message.js       # Message schema
├── routes/
│   ├── auth.js          # Authentication routes
│   ├── products.js      # Product CRUD routes
│   ├── messages.js      # Messaging routes
│   └── admin.js         # Admin management routes
├── middleware/
│   └── auth.js          # JWT authentication middleware
├── server.js            # Main server file
├── package.json
├── .env.example
└── README.md
```

## 🔌 API Endpoints

### Authentication

- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user (Protected)

### Products

- `GET /api/products` - Get all products (Public)
- `GET /api/products/my-products` - Get farmer's products (Farmer only)
- `POST /api/products` - Create product (Farmer only)
- `PUT /api/products/:id` - Update product (Farmer only)
- `DELETE /api/products/:id` - Delete product (Farmer only)

### Messages

- `POST /api/messages` - Send message to farmer (Buyer only)
- `GET /api/messages/farmer` - Get farmer's messages (Farmer only)
- `GET /api/messages/buyer` - Get buyer's messages (Buyer only)
- `PATCH /api/messages/:id/read` - Mark as read (Farmer only)

### Admin

- `GET /api/admin/users` - Get all users (Admin only)
- `GET /api/admin/products` - Get all products (Admin only)
- `PATCH /api/admin/users/:id/approve` - Approve user (Admin only)
- `DELETE /api/admin/users/:id` - Delete user (Admin only)
- `DELETE /api/admin/products/:id` - Delete product (Admin only)
- `PATCH /api/admin/products/:id/approve` - Approve product (Admin only)

## 🔐 Authentication

The API uses JWT (JSON Web Tokens) for authentication. Include the token in the Authorization header:

```
Authorization: Bearer <your_jwt_token>
```

## 👥 User Roles

1. **Farmer** - Can add, edit, delete their products and receive messages
2. **Buyer** - Can browse products and send messages to farmers
3. **Admin** - Can manage all users and products

## 🗃️ Database Models

### User Model

```javascript
{
  name: String,
  email: String (unique),
  password: String (hashed),
  role: String (farmer/buyer/admin),
  phone: String,
  location: String,
  approved: Boolean,
  createdAt: Date
}
```

### Product Model

```javascript
{
  name: String,
  category: String (Vegetables/Fruits/Dairy/Cereals),
  price: Number,
  quantity: Number,
  unit: String (kg/lbs/units/liters),
  description: String,
  image: String,
  farmer: ObjectId (ref: User),
  approved: Boolean,
  createdAt: Date
}
```

### Message Model

```javascript
{
  buyer: ObjectId (ref: User),
  farmer: ObjectId (ref: User),
  product: ObjectId (ref: Product),
  message: String,
  read: Boolean,
  createdAt: Date
}
```

## 🧪 Testing the API

You can test the API using:

- **Postman** - Import the endpoints and test
- **Thunder Client** (VS Code extension)
- **cURL** commands

Example login request:

```bash
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"farmer@test.com","password":"password123"}'
```

## 🛠️ Development Tips

1. **Create an admin user manually in MongoDB:**

```javascript
// In MongoDB shell or Compass
db.users.insertOne({
  name: "Admin User",
  email: "admin@agrismart.com",
  password: "$2a$10$...", // Use bcrypt to hash password
  role: "admin",
  phone: "1234567890",
  location: "HQ",
  approved: true,
  createdAt: new Date()
})
```

2. **Watch for errors in console** - All errors are logged

3. **MongoDB Connection Issues?**
   - Check if MongoDB is running
   - Verify connection string in .env
   - For Atlas, check IP whitelist

## 📝 Environment Variables

Required variables in `.env`:

- `PORT` - Server port (default: 5000)
- `NODE_ENV` - Environment (development/production)
- `MONGODB_URI` - MongoDB connection string
- `JWT_SECRET` - Secret key for JWT tokens
- `CORS_ORIGIN` - Frontend URL for CORS

## 🚢 Deployment

For production deployment:

1. Set `NODE_ENV=production` in .env
2. Use a strong `JWT_SECRET`
3. Use MongoDB Atlas for database
4. Deploy to platforms like:
   - Heroku
   - Railway
   - Render
   - DigitalOcean
   - AWS/Azure/GCP

## 📧 Support

For issues or questions, check the console logs or refer to the API documentation.

Happy Coding! 🌱