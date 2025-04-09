# Zynetic Backend - BookStore API

## Description

This BookStore API is a RESTful web service designed for managing users and books within a bookstore system. It enables users to register, log in, and view available books. Additionally, the API implements role-based access control, ensuring that only users with admin privileges can create, update, or delete books. Regular users have read-only access, making the system secure and well-structured for managing both users and book inventory.

## Funtions

- User registration and authentication
- Role-based access control (admin and normal users)
- CRUD operations for books
- Swagger/OpenAPI documentation
- Unit and integration tests

## Technologies Used

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

### Prerequisites

- Node.js (v12 or higher)
- MongoDB

### Implementation

1. Clone the repository
   `git clone https://github.com/ananyab1909/Zynetic-Backend.git`

2. Enter into the directory
   `cd Zynetic-Backend`

3. Install the dependencies
   `npm install`

4. Prepare the project’s environment variables

   Place the following content in a new file named `default.json` under the config folder:
   
   `{
     "mongoURI": "your_mongodb_connection_string",
     "jwtSecret": "your_jwt_secret",
     "admin-signup-key": "your_admin_signup_key"
   }`

6. Kickstart the server:
   npm start

The server will start on `http://localhost:3000`.

### API Docs

The API documentation is available at `http://localhost:3000/api-docs`.

### User Routes

#### Sign Up - User Registration

- **URL:** `/api/users/register`
- **Method:** `POST`
- **Request Body:**

  `{
    "name": "John Doe",
    "email": "john.doe@example.com",
    "password": "password1234"
  }`

- **Response:**
  `{
    "token": "jwt_token"
  }`

#### Login - Only signed up users

- **URL:** `/api/users/login`
- **Method:** `POST`
- **Request Body:**
  `{
    "email": "john.doe@example.com",
    "password": "password1234"
  }`

- **Response:**
  `{
    "token": "jwt_token"
  }`

### CRUD Operations

#### Retrieve All Books

- **URL:** `/api/books`
- **Method:** `GET`
- **Query Parameters:**
  - `category` (optional)
  - `author` (optional)
  - `rating` (optional)
  - `page` (optional, default: 1)
  - `limit` (optional, default: 10)

- **Response:**
  `{
  "currentPage": 1,
  "totalPages": 1,
  "books": [
    {
      "title": "The Palace of Illusions",
      "description": "A retelling of the Mahabharata through the eyes of Draupadi, the fiery queen.",
      "price": 750,
      "stock": 50,
      "category": "Mythological Fiction",
      "author": "Chitra Banerjee Divakaruni",
      "rating": 4.8
    },
    {
      "title": "Wings of Fire",
      "description": "An inspiring autobiography of A.P.J. Abdul Kalam, former President of India and a renowned scientist.",
      "price": 450,
      "stock": 200,
      "category": "Autobiography",
      "author": "A.P.J. Abdul Kalam",
      "rating": 4.9
    }
  ]
}`


#### Book Retrieve by ID

- **URL:** `/api/books/{bookId}`
- **Method:** `GET`
- **Response:** 
`{
  "title": "The Palace of Illusions",
  "description": "A reimagining of the Mahabharata from Draupadi's perspective, blending myth, history, and feminism.",
  "price": 750,
  "stock": 60,
  "category": "Mythological Fiction",
  "author": "Chitra Banerjee Divakaruni",
  "rating": 4.8
}`


#### Insert book entry

- **URL:** `/api/books`
- **Method:** `POST`
- **Headers:**
  - `x-auth-token`: `jwt_token`
- **Request Body:**
`{
  "title": "The Palace of Illusions",
  "description": "A reimagining of the Mahabharata from Draupadi's perspective, blending myth, history, and feminism.",
  "price": 750,
  "stock": 60,
  "category": "Mythological Fiction",
  "author": "Chitra Banerjee Divakaruni",
  "rating": 4.8
}`

- **Response:** 
  `{
    "newBook": {
      "title": "The Palace of Illusions",
        "description": "A reimagining of the Mahabharata from Draupadi's perspective, blending myth, history, and feminism.",
        "price": 750,
        "stock": 60,
        "category": "Mythological Fiction",
        "author": "Chitra Banerjee Divakaruni",
        "rating": 4.8
    }
  }`

#### Edit book entry

- **URL:** `/api/books/{bookId}`
- **Method:** `PATCH`
- **Headers:**
  - `x-auth-token`: `jwt_token`
- **Request Body:**
  `{
    "price": 200
  }`

- **Response:**
  `{
    "message": "Successfully updated the book"
  }`
  
#### Remove book entry

- **URL:** `/api/books/{bookId}`
- **Method:** `DELETE`
- **Headers:**
  - `x-auth-token`: `jwt_token`
- **Response:**
  `{
    "message": "Successfully deleted the book"
  }`

### Integration and Unit Tests

1. Install libraries needed for development
   `npm install --save-dev mocha chai chai-http`

2. Trigger test execution:
   `npm test`

### Code Testing
- **User Tests:** __Zynetic-Backend/test/user.js__
- **Book Tests:** __Zynetic-Backend/test/book.js__

## License

This project is licensed under the MIT License.
