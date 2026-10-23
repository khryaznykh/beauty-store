# Beauty Store — Backend API

A RESTful backend API for a full-stack e-commerce application built with **Node.js, Express.js, MongoDB, and Mongoose**.

The backend handles user authentication, product management, customer reviews, and user account operations. It is designed to support a React frontend and uses JWT-based authentication to protect private API endpoints.

**Project Status:** Active Development

## Tech Stack

| Technology | Purpose |
|---|---|
| Node.js | JavaScript runtime |
| Express.js | REST API and middleware |
| MongoDB Atlas | Cloud-hosted database |
| Mongoose | Database schemas and queries |
| JSON Web Token (JWT) | Authentication and protected API access |
| bcrypt | Password hashing |
| CORS | Cross-origin API access |
| dotenv | Environment variable management |

**Frontend:** React, Vite, Redux Toolkit, RTK Query, React Hook Form, React Context API

**Deployment:** Render (backend), Netlify (frontend), MongoDB Atlas (database)

## Architecture

The backend follows a modular structure with separate responsibilities for routing, request handling, business logic, and database operations.

- **Routes:** Define API endpoints and attach middleware.
- **Controllers:** Handle HTTP requests, responses, and errors.
- **Services:** Implement reusable business logic.
- **Models:** Define MongoDB document structures using Mongoose.
- **Middleware:** Validate JWTs and control access to protected endpoints.

This separation improves code organization, maintainability, and extensibility.

## Authentication and Authorization

The application implements JWT-based authentication with server-side token verification.

### Authentication Flow

1. A user registers with their account information.
2. The password is hashed using bcrypt before being stored in MongoDB.
3. During sign-in, the backend validates the supplied credentials.
4. After successful authentication, the server generates a signed JWT containing user information.
5. The frontend stores the access token and includes it in protected API requests.
6. Authentication middleware extracts the token from the `Authorization` header.
7. The backend verifies the token using `jwt.verify()` and the configured JWT secret.
8. After successful verification, the decoded user information is attached to `req.user` for use by protected controllers.

Example authenticated request:

```http
GET /profile
Authorization: Bearer <access_token>
```

### Authentication Features

- User registration and sign-in
- Password hashing with bcrypt
- JWT access-token generation
- Token signature and expiration verification
- Authentication middleware for protected endpoints
- Authenticated user identification through `req.user`
- Access control for user-specific operations

The current authentication implementation uses Bearer tokens. The frontend manages token expiration and login state.

### Security Considerations

- Passwords are stored as hashes rather than plaintext.
- JWT signatures are verified on the server.
- Protected routes require a valid access token.
- Authentication secrets and database credentials are configured through environment variables.
- User-specific operations are designed to associate data with the authenticated user.

**Planned improvements:** More comprehensive role-based authorization, stronger session management, and backend-managed HttpOnly authentication cookies.

## API Features

### Products

Product endpoints support the application's product catalog and individual product pages.

Implemented backend operations include:

- Create a product
- Retrieve all products
- Retrieve a product by ID
- Update product information

Product data is managed through Mongoose models and stored in MongoDB.

### Customer Reviews

The review system is designed to associate customer feedback with both a product and a registered user.

Review data includes:

- Product reference
- User reference
- Rating
- Review headline
- Review text
- Recommendation
- Publication status

The backend includes review operations for creating reviews, retrieving user-specific reviews, and managing review records.

A review moderation workflow is being developed to control which reviews are publicly visible.

### User Accounts

The backend includes functionality for retrieving authenticated user profile information and supporting user-specific account operations.

Additional profile management and purchase history features are planned.

## API Endpoints

The following table documents the core API routes and review routes developed or discussed for this project. Review endpoint availability and exact methods should be verified against the current route files before treating this as the final API reference.

| Method | Endpoint | Description |
|---|---|---|
| POST | `/signin` | Authenticate a user |
| POST | `/signup` | Register a user |
| GET | `/profile` | Retrieve authenticated user profile |
| GET | `/products` | Retrieve products |
| GET | `/products/:id` | Retrieve a product by ID |
| POST | `/products` | Create a product |
| PUT | `/products/:id` | Update a product |
| POST | `/products/:id/reviews` | Submit a product review |
| GET | `/account/my-reviews` | Retrieve the current user's reviews |
| PATCH | `/account/my-reviews/:id` | Update a user's review |
| DELETE | `/account/my-reviews/:id` | Delete a user's review |

Authentication is required for protected account and review operations.

Administrative endpoint documentation will be expanded as the admin functionality is finalized.

## Database Design

The application uses MongoDB with Mongoose to model and manage application data.

### User

Stores account information and securely hashed passwords.

### Product

Stores product information used by the storefront and product detail pages.

### Review

Stores product feedback with references to the associated product and user.

Mongoose `ObjectId` references establish relationships between review documents and their related users and products.

## Running Locally

### Prerequisites

- Node.js and npm
- MongoDB database connection
- Required environment variables

### Installation

Clone the repository:

```bash
git clone https://github.com/khryaznykh/beauty-store-backend.git
cd beauty-store-backend
```

Install dependencies:

```bash
npm install
```

Create a `.env` file and configure the environment variables used by the application.

Example:

```env
PORT=8000
JWT_SECRET=your_secure_jwt_secret
```

Add the MongoDB connection variable required by your database configuration.

Start the server using the development or start script defined in `package.json`.

Never commit `.env` files, database credentials, or JWT secrets to version control.

## Current Development Status

### Implemented

- Express REST API architecture
- MongoDB and Mongoose integration
- User registration and sign-in logic
- Password hashing
- JWT generation and verification
- Authentication middleware
- Product CRUD operations (partial)
- User profile retrieval endpoint
- Review models and review-related backend logic
- Frontend integration through RTK Query
- Cloud deployment on Render

### In Progress / Requires Further Testing

- Complete customer review lifecycle
- Published-only review retrieval
- Review moderation and administrative workflows
- Role-based authorization for administrative endpoints
- Consistent error handling and HTTP status codes
- Validation and authorization across all write operations

## Planned Features

- **Admin API:** Secure endpoints for product, user, review, and order management.
- **Stripe Integration:** Server-side checkout session creation, payment processing integration, and webhook handling.
- **Order Management:** Order creation, purchase records, order history, and order status tracking.
- **Enhanced User Profiles:** Profile editing, account settings, and additional user-specific functionality.
- **Authentication Improvements:** Improved token handling and secure session management.
- **Automated Testing:** Unit and integration tests for controllers, services, authentication, and API endpoints.
- **API Documentation:** Complete endpoint documentation with request and response examples.

## Related Repository

**Frontend:** https://github.com/khryaznykh/beauty-store-frontend

## Project Overview

Beauty Store is an ongoing full-stack portfolio project demonstrating practical experience with REST API development, database modeling, JWT authentication, password security, middleware, modular backend architecture, and integration with a modern React frontend.

The project continues to evolve toward a more complete e-commerce platform with administrative tools, secure checkout, and expanded customer account functionality.
