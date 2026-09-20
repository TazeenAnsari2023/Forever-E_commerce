# Forever — Full-Stack E-commerce

Forever is a full-stack fashion e-commerce application built with **React + Vite**, **Node.js + Express**, **MongoDB**, and an **Admin Dashboard**.

The project is organized into three applications:

- `frontend/` → customer-facing React storefront
- `backend/` → Express REST API, authentication, products, cart, and orders
- `admin/` → React/Vite admin dashboard for product and order management

> This repository uses a separate frontend, backend, and admin application architecture. The frontend and admin are Vite applications, while the backend is an Express server.

## Project Structure

```text
forever-full-stack/
├── frontend/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/
│   │   ├── context/
│   │   └── pages/
│   ├── public/
│   ├── package.json
│   └── .env
│
├── backend/
│   ├── config/
│   │   ├── cloudinary.js
│   │   └── mongodb.js
│   ├── controllers/
│   │   ├── cartController.js
│   │   ├── orderController.js
│   │   ├── productController.js
│   │   └── userController.js
│   ├── middleware/
│   │   ├── adminAuth.js
│   │   ├── auth.js
│   │   └── multer.js
│   ├── models/
│   │   ├── orderModel.js
│   │   ├── productModel.js
│   │   └── userModel.js
│   ├── routes/
│   │   ├── cartRoute.js
│   │   ├── orderRoute.js
│   │   ├── productRoute.js
│   │   └── userRoute.js
│   ├── server.js
│   ├── package.json
│   └── .env
│
└── admin/
    ├── src/
    │   ├── components/
    │   ├── pages/
    │   └── assets/
    ├── package.json
    └── .env
```

## Features

### Customer Storefront

- Responsive fashion e-commerce interface
- Product collections and best sellers
- Product details with images and sizes
- Category and sub-category browsing
- Shopping cart
- User registration and login
- Persistent authentication token
- Order placement
- Order history and status display
- Cash on Delivery
- Stripe payment integration
- Razorpay payment integration
- Product image hosting through Cloudinary
- Toast notifications for user feedback

### Admin Dashboard

- Admin authentication
- Add products
- Upload product images
- Product listing
- Product management
- Order listing
- Order status management
- Backend API integration

### Backend API

The Express backend provides REST endpoints for:

```text
/api/user/*
/api/product/*
/api/cart/*
/api/order/*
```

The backend uses:

- Express
- MongoDB / Mongoose
- JWT authentication
- bcrypt password hashing
- Cloudinary
- Multer
- Stripe
- Razorpay
- CORS
- dotenv

## Technology Stack

### Frontend

- React 18
- Vite
- React Router
- Axios
- React Toastify
- Tailwind CSS

### Backend

- Node.js
- Express
- MongoDB
- Mongoose
- JWT
- bcrypt
- Cloudinary
- Multer
- Stripe
- Razorpay

### Admin

- React 18
- Vite
- React Router
- Axios
- Tailwind CSS
- React Toastify

## Local Development

You need Node.js and MongoDB access before starting the application.

### 1. Install frontend dependencies

```bash
cd frontend
npm install
```

### 2. Install backend dependencies

```bash
cd ../backend
npm install
```

### 3. Install admin dependencies

```bash
cd ../admin
npm install
```

## Environment Variables

Never commit real API keys, database passwords, payment secrets, or JWT secrets to Git.

### Backend `.env`

Create:

```text
backend/.env
```

with:

```env
JWT_SECRET=your_jwt_secret
ADMIN_EMAIL=your_admin_email
ADMIN_PASSWORD=your_admin_password

MONGODB_URI=your_mongodb_connection_string

CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_SECRET_KEY=your_cloudinary_secret_key
CLOUDINARY_NAME=your_cloudinary_cloud_name

STRIPE_SECRET_KEY=your_stripe_secret_key

RAZORPAY_KEY_SECRET=your_razorpay_secret_key
RAZORPAY_KEY_ID=your_razorpay_key_id
```

### Frontend `.env`

Create:

```text
frontend/.env
```

with:

```env
VITE_BACKEND_URL=http://localhost:4000
VITE_RAZORPAY_KEY_ID=your_razorpay_key_id
```

### Admin `.env`

Create:

```text
admin/.env
```

with:

```env
VITE_BACKEND_URL=http://localhost:4000
```

Use the same backend URL for the frontend and admin during local development.

## Running the Project

The project has three processes.

### Terminal 1 — Backend

```bash
cd backend
npm run server
```

The API runs on:

```text
http://localhost:4000
```

The backend also exposes:

```text
GET /
```

which returns:

```text
API Working
```

### Terminal 2 — Customer Frontend

```bash
cd frontend
npm run dev
```

Vite will display the local frontend URL in the terminal.

### Terminal 3 — Admin Dashboard

```bash
cd admin
npm run dev
```

Vite will display the local admin URL in the terminal.

## Production Builds

### Frontend

```bash
cd frontend
npm run build
```

Preview the production build:

```bash
npm run preview
```

### Admin

```bash
cd admin
npm run build
```

Preview the production build:

```bash
npm run preview
```

### Backend

Start the production server with:

```bash
cd backend
npm start
```

The server uses:

```js
process.env.PORT || 4000
```

## API Routes

### User

```text
POST /api/user/register
POST /api/user/login
```

### Products

```text
GET /api/product/list
POST /api/product/add
POST /api/product/remove
```

### Cart

```text
POST /api/cart/get
POST /api/cart/add
POST /api/cart/update
```

### Orders

```text
POST /api/order/place
POST /api/order/userorders
POST /api/order/list
POST /api/order/status
POST /api/order/stripe
POST /api/order/verifyStripe
POST /api/order/razorpay
POST /api/order/verifyRazorpay
```

> Exact request bodies and authentication requirements should be checked against the corresponding route/controller files when integrating another client.

## Authentication

Customer authentication uses JWT.

After login or registration, the frontend stores the returned token in browser storage and sends it to protected API endpoints using the `token` request header.

Admin-protected routes use separate admin authentication middleware.

## Payments

Forever supports three order payment methods:

1. **Cash on Delivery**
2. **Stripe**
3. **Razorpay**

Payment secrets must remain server-side.

Only public/client-safe payment configuration should be exposed through Vite environment variables such as:

```env
VITE_RAZORPAY_KEY_ID=...
```

Never expose:

```text
RAZORPAY_KEY_SECRET
STRIPE_SECRET_KEY
JWT_SECRET
MONGODB_URI
CLOUDINARY_SECRET_KEY
```

to the browser.

## Database

MongoDB is used for application data.

The backend connects using:

```env
MONGODB_URI=...
```

The main data models are:

- User
- Product
- Order

Cart data is also handled through the user/cart backend flow.

## Cloudinary

Product images are uploaded and managed through Cloudinary.

Required backend configuration:

```env
CLOUDINARY_API_KEY=...
CLOUDINARY_SECRET_KEY=...
CLOUDINARY_NAME=...
```

## Deployment

Because this repository contains three separate applications, deployment can be handled as separate services.

### Recommended deployment layout

```text
Customer Frontend
        │
        ▼
   Vite Hosting
        │
        ▼
Express Backend ─── MongoDB
        │
        ├── Cloudinary
        ├── Stripe
        └── Razorpay

Admin Dashboard
        │
        ▼
   Vite Hosting
        │
        ▼
Express Backend
```

### Backend deployment

Deploy the `backend/` directory to a Node.js-compatible service.

Configure:

```env
PORT=4000
JWT_SECRET=...
ADMIN_EMAIL=...
ADMIN_PASSWORD=...
MONGODB_URI=...
CLOUDINARY_API_KEY=...
CLOUDINARY_SECRET_KEY=...
CLOUDINARY_NAME=...
STRIPE_SECRET_KEY=...
RAZORPAY_KEY_SECRET=...
RAZORPAY_KEY_ID=...
```

After deployment, use the deployed API URL as:

```env
VITE_BACKEND_URL=https://your-backend-domain.example
```

for both frontend and admin.

### Frontend deployment

Build from the `frontend/` directory:

```bash
npm install
npm run build
```

Set:

```env
VITE_BACKEND_URL=https://your-backend-domain.example
VITE_RAZORPAY_KEY_ID=...
```

### Admin deployment

Build from the `admin/` directory:

```bash
npm install
npm run build
```

Set:

```env
VITE_BACKEND_URL=https://your-backend-domain.example
```

## CORS

The backend currently enables CORS through Express.

For production, configure CORS to allow only the domains that should access your API rather than relying on a permissive production configuration.

## Security Checklist

Before deploying:

- [ ] Remove real `.env` files from Git history if they were committed.
- [ ] Rotate any exposed database credentials.
- [ ] Rotate exposed payment API secrets.
- [ ] Generate a strong JWT secret.
- [ ] Use HTTPS for production frontend, admin, and API.
- [ ] Restrict production CORS origins.
- [ ] Keep Stripe/Razorpay secret keys on the backend only.
- [ ] Keep MongoDB credentials server-side.
- [ ] Do not expose Cloudinary API secrets to the frontend.
- [ ] Configure production payment webhooks/verification according to the payment provider's requirements.

## Useful Commands

### Frontend

```bash
cd frontend
npm install
npm run dev
npm run build
npm run preview
npm run lint
```

### Backend

```bash
cd backend
npm install
npm run server
npm start
```

### Admin

```bash
cd admin
npm install
npm run dev
npm run build
npm run preview
npm run lint
```

## Project Status

**Forever** is a full-stack e-commerce project containing:

- Customer shopping experience
- Authentication
- Product catalog
- Cart management
- Order management
- Admin dashboard
- MongoDB persistence
- Cloudinary image management
- Stripe payments
- Razorpay payments
- Responsive React interfaces

## License

This project does not currently declare a specific open-source license. If you plan to publish or distribute it, add an appropriate `LICENSE` file and update this section.

---

# Forever E-commerce

**Frontend + Backend + Admin Dashboard**

Built with React, Vite, Express, MongoDB, Cloudinary, Stripe, and Razorpay.
