# Go Backend API

A lightweight e-commerce backend API built with Go, providing essential functionality for user management, product management, and order processing.

## Features

- **User Management**: Registration, authentication, and JWT-based access control
- **Product Management**: Create, read, update products with inventory tracking
- **Cart & Checkout**: Shopping cart functionality with checkout process
- **Order Processing**: Order creation and management

## Tech Stack

- **Go**: Core language
- **MySQL**: Database
- **Gorilla Mux**: HTTP routing
- **SQL Migrations**: Database schema management

## Project Structure

```
├── cmd/
│   ├── api/            # API server implementation
│   ├── migrate/        # Database migration tools
│   └── main.go         # Application entry point
├── configs/            # Configuration management
├── db/                 # Database connection setup
├── services/           # Business logic organized by domain
│   ├── auth/           # Authentication service
│   ├── cart/           # Shopping cart service
│   ├── order/          # Order processing service
│   ├── product/        # Product management service
│   └── user/           # User management service
├── types/              # Shared data types
└── utils/              # Utility functions
```

## Getting Started

### Prerequisites

- Go 1.19 or later
- MySQL 5.7 or later

### Installation

1. Clone the repository:
   ```
   git clone https://github.com/fawwazmw/go-backend-api.git
   cd go-backend-api
   ```

2. Set up environment variables (or use the default .env file):
   ```
   # Server
   PUBLIC_HOST=http://localhost
   PORT=8080

   # Database
   DB_USER=your_db_user
   DB_PASSWORD=your_db_password
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_NAME=go_backend_db
   ```

3. Create the database:
   ```sql
   CREATE DATABASE go_backend_db;
   ```

4. Run the migrations:
   ```
   make migrate-up
   ```

5. Build and run the application:
   ```
   make run
   ```

## API Endpoints

### Authentication

- `POST /api/v1/register` - Register a new user
  ```json
  {
    "firstName": "Budiono",
    "lastName": "Siregar",
    "email": "budiono@example.com",
    "password": "budiganteng123"
  }
  ```

- `POST /api/v1/login` - Login and get JWT token
  ```json
  {
    "email": "budiono@example.com",
    "password": "budiganteng123"
  }
  ```

### Products

- `GET /api/v1/products` - Get all products
- `GET /api/v1/products/{productID}` - Get a specific product
- `POST /api/v1/products` - Create a new product (requires authentication)
  ```json
  {
    "name": "Product Name",
    "description": "Product description",
    "image": "product-image.jpg",
    "price": 19.99,
    "quantity": 100
  }
  ```

### Cart & Checkout

- `POST /api/v1/cart/checkout` - Process checkout (requires authentication)
  ```json
  {
    "items": [
      {
        "productID": 1,
        "quantity": 2
      },
      {
        "productID": 3,
        "quantity": 1
      }
    ]
  }
  ```

## Development

### Database Migrations

Create a new migration:
```
make migration migration_name
```

Apply migrations:
```
make migrate-up
```

Rollback migrations:
```
make migrate-down
```

### Running Tests

Run all tests:
```
make test
```

## Project Design Decisions

- **Repository Pattern**: Separation of data access layer from business logic
- **Dependency Injection**: Enables testability and modularity
- **JWT Authentication**: Stateless authentication for API endpoints
- **SQL Transactions**: Used for critical operations like checkout to maintain data integrity
- **Validators**: Input validation to ensure data integrity

## Future Improvements

- Add pagination for product listings
- Implement role-based access control
- Add search and filtering capabilities
- Introduce caching for frequently accessed data
- Implement webhooks for order status updates
- Add support for product categories and tags

## License

This project is licensed under the [MIT License](https://opensource.org/license/MIT) - see the LICENSE file for details.