# Zynetic Backend - BookStore API

## Table of Contents

- [Description](#description)
- [Features](#features)
- [Technologies](#technologies)
- [Setup Instructions](#setup-instructions)
- [API Documentation](#api-documentation)
- [Testing](#testing)
- [License](#license)

## Description

This BookStore API is a RESTful web service designed for managing users and books within a bookstore system. It enables users to register, log in, and view available books. Additionally, the API implements role-based access control, ensuring that only users with admin privileges can create, update, or delete books. Regular users have read-only access, making the system secure and well-structured for managing both users and book inventory.

## Features

- User registration and authentication
- Role-based access control (admin and normal users)
- CRUD operations for books
- Swagger/OpenAPI documentation
- Unit and integration tests

## Technologies

- Node.js
- Express.js
- MongoDB
- Mongoose
- JWT (JSON Web Tokens)
- bcrypt.js
- Swagger
- Mocha
- Chai
- Chai-HTTP

## Setup Instructions

### Prerequisites

- Node.js (v12 or higher)
- MongoDB

### Installation

1. Clone the repository:
   git clone https://github.com/yourusername/Zynetic-Backend.git
   cd Zynetic-Backend


2. Install dependencies:
   npm install

3. Set up environment variables:

   Create a `default.json` file in the config directory with the following content:

   {
     "mongoURI": "your_mongodb_connection_string",
     "jwtSecret": "your_jwt_secret",
     "admin-signup-key": "your_admin_signup_key"
   }


4. Start the server:
   npm start


   __The server will start on `http://localhost:3000`.__

### API Documentation

The API documentation is available at `http://localhost:3000/api-docs`.

### User Routes

#### Sign Up - User Registration

- **URL:** `/api/users/register`
- **Method:** `POST`
- **Request Body:**

  {
    "name": "John Doe",
    "email": "john.doe@example.com",
    "password": "password1234"
  }

- **Response:**
  {
    "token": "jwt_token"
  }

#### Login - Only signed up users

- **URL:** `/api/users/login`
- **Method:** `POST`
- **Request Body:**

  {
    "email": "john.doe@example.com",
    "password": "password1234"
  }

- **Response:**

  {
    "token": "jwt_token"
  }

### Book Routes

#### Get All Books

- **URL:** `/api/books`
- **Method:** `GET`
- **Query Parameters:**
  - `category` (optional)
  - `author` (optional)
  - `rating` (optional)
  - `page` (optional, default: 1)
  - `limit` (optional, default: 10)

- **Response:**

  {
    "books": [

  {
        "title": "Malgudi Days",
        "description": "A collection of short stories",
        "price": 500,
        "stock": 100,
        "category": "Fiction",
        "author": "R.K. Narayan",
        "rating": 4.5
  }
    ],
    "totalPages": 1,
    "currentPage": 1
  }


#### Get a Book by ID

- **URL:** `/api/books/{bookId}`
- **Method:** `GET`
- **Response:**
 
  {
    "title": "Malgudi Days",
    "description": "A collection of short stories",
    "price": 500,
    "stock": 100,
    "category": "Fiction",
    "author": "R.K. Narayan",
    "rating": 4.5
  }

#### Create a Book

- **URL:** `/api/books`
- **Method:** `POST`
- **Headers:**
  - `x-auth-token`: `jwt_token`
- **Request Body:**

  {
    "title": "Malgudi Days",
    "description": "A collection of short stories",
    "price": 500,
    "stock": 100,
    "category": "Fiction",
    "author": "R.K. Narayan",
    "rating": 4.5
  }

- **Response:**
  
  {
    "newBook": {
      "title": "Malgudi Days",
      "description": "A collection of short stories",
      "price": 500,
      "stock": 100,
      "category": "Fiction",
      "author": "R.K. Narayan",
      "rating": 4.5
    }
  }

#### Update a Book

- **URL:** `/api/books/{bookId}`
- **Method:** `PATCH`
- **Headers:**
  - `x-auth-token`: `jwt_token`
- **Request Body:**

  {
    "price": 600
  }

- **Response:**

  {
    "message": "Successfully updated the book"
  }

#### Delete a Book

- **URL:** `/api/books/{bookId}`
- **Method:** `DELETE`
- **Headers:**
  - `x-auth-token`: `jwt_token`
- **Response:**

  {
    "message": "Successfully deleted the book"
  }

## Testing

### Running Integration and Unit Tests

1. Install development dependencies:

   npm install --save-dev mocha chai chai-http

2. Run the tests:

   npm test

### Test Codes

- **User Tests:** __Zynetic-Backend/test/user.js__
- **Book Tests:** __Zynetic-Backend/test/book.js__

## License

This project is licensed under the MIT License.
