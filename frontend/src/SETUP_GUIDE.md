# AgriSmart - Setup Guide

## 🎯 Quick Start (Demo Mode)

The application is currently running in **Demo Mode** with sample data. You can explore all features without setting up a backend!

### Demo Credentials

Use these credentials to login and test different user roles:

- **Farmer Account**
  - Email: `farmer@demo.com`
  - Password: `demo123`
  - Features: Add/edit/delete products, view messages from buyers

- **Buyer Account**
  - Email: `buyer@demo.com`
  - Password: `demo123`
  - Features: Browse products, filter by category, contact farmers

- **Admin Account**
  - Email: `admin@demo.com`
  - Password: `demo123`
  - Features: Manage all users and products, approve/delete items

## 🚀 Setting Up the Full Backend

To enable full functionality with real database and authentication:

### 1. Install MongoDB

**Option A: Local MongoDB**
```bash
# Download and install from https://www.mongodb.com/try/download/community
# Or use Homebrew (Mac)
brew install mongodb-community

# Start MongoDB
mongod
```

**Option B: MongoDB Atlas (Cloud - Recommended)**
1. Go to https://www.mongodb.com/cloud/atlas
2. Create a free account
3. Create a new cluster
4. Get your connection string

### 2. Setup Backend

```bash
# Navigate to backend folder
cd backend

# Install dependencies
npm install

# Create environment file
cp .env.example .env

# Edit .env file and add your MongoDB URI
# For local: MONGODB_URI=mongodb://localhost:27017/agrismart
# For Atlas: MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/agrismart
```

### 3. Start the Backend Server

```bash
# Development mode (auto-reload)
npm run dev

# Or production mode
npm start
```

The backend will run on `http://localhost:5000`

### 4. Test the Connection

Once your backend is running:
1. Refresh the frontend application
2. Try registering a new account
3. The demo banner will disappear once real backend is connected

## 📁 Project Structure

```
agrismart/
├── backend/                    # Node.js + Express + MongoDB backend
│   ├── models/                 # Database schemas
│   │   ├── User.js
│   │   ├── Product.js
│   │   └── Message.js
│   ├── routes/                 # API endpoints
│   │   ├── auth.js
│   │   ├── products.js
│   │   ├── messages.js
│   │   └── admin.js
│   ├── middleware/
│   │   └── auth.js             # JWT authentication
│   ├── server.js               # Main server file
│   └── package.json
│
├── components/                 # React components
│   ├── HomePage.tsx
│   ├── LoginPage.tsx
│   ├── SignupPage.tsx
│   ├── FarmerDashboard.tsx
│   ├── BuyerDashboard.tsx
│   ├── AdminPanel.tsx
│   └── Navbar.tsx
│
├── utils/
│   └── mockData.ts             # Demo data (used when backend is offline)
│
└── App.tsx                     # Main app component
```

## 🔌 API Endpoints

Once your backend is running, these endpoints will be available:

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user (protected)

### Products
- `GET /api/products` - Get all products
- `GET /api/products/my-products` - Get farmer's products (farmer only)
- `POST /api/products` - Create product (farmer only)
- `PUT /api/products/:id` - Update product (farmer only)
- `DELETE /api/products/:id` - Delete product (farmer only)

### Messages
- `POST /api/messages` - Send message (buyer only)
- `GET /api/messages/farmer` - Get farmer's messages (farmer only)
- `GET /api/messages/buyer` - Get buyer's messages (buyer only)

### Admin
- `GET /api/admin/users` - Get all users (admin only)
- `GET /api/admin/products` - Get all products (admin only)
- `PATCH /api/admin/users/:id/approve` - Approve user (admin only)
- `DELETE /api/admin/users/:id` - Delete user (admin only)
- `DELETE /api/admin/products/:id` - Delete product (admin only)

## 🛠️ Technology Stack

### Frontend
- **React** - UI framework
- **TypeScript** - Type safety
- **Tailwind CSS** - Styling
- **Lucide React** - Icons

### Backend
- **Node.js** - Runtime
- **Express** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM
- **JWT** - Authentication
- **bcryptjs** - Password hashing

## 📝 Environment Variables

Create a `.env` file in the backend folder:

```env
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb://localhost:27017/agrismart
JWT_SECRET=your_super_secret_key_change_this
CORS_ORIGIN=http://localhost:3000
```

## 🐛 Troubleshooting

### Backend won't connect
- Make sure MongoDB is running
- Check your MONGODB_URI in .env
- Verify port 5000 is not in use

### CORS errors
- Update CORS_ORIGIN in backend .env
- Make sure backend is running before frontend

### Demo mode won't disable
- Check if backend is actually running on port 5000
- Clear browser localStorage and refresh
- Check browser console for connection errors

## 🚢 Deployment

### Backend Deployment (Choose one)
- **Heroku**: https://www.heroku.com
- **Railway**: https://railway.app
- **Render**: https://render.com
- **DigitalOcean**: https://www.digitalocean.com

### Frontend Deployment
- Already running in Figma Make!
- Or deploy to Vercel, Netlify, etc.

### Production Checklist
- [ ] Set strong JWT_SECRET
- [ ] Use MongoDB Atlas for database
- [ ] Set NODE_ENV=production
- [ ] Enable HTTPS
- [ ] Set up proper CORS origins
- [ ] Add rate limiting
- [ ] Set up logging and monitoring

## 💡 Next Steps

1. **Extend Features**
   - Add image upload for products
   - Implement real-time chat
   - Add payment integration
   - Create order management system

2. **Improve Security**
   - Add email verification
   - Implement password reset
   - Add two-factor authentication
   - Rate limiting on API calls

3. **Enhance UI/UX**
   - Add loading skeletons
   - Implement infinite scroll
   - Add product reviews/ratings
   - Create mobile app version

## 📧 Support

For questions or issues:
- Check the backend README.md
- Review API documentation
- Check MongoDB connection
- Verify all environment variables

Happy farming! 🌱
