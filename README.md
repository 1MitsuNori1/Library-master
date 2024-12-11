# Library with JWT Authentication

Welcome to the **Library Management System**! This robust solution leverages **JSON Web Tokens (JWT)** for secure, role-based access control while enabling streamlined management of books and authors. Designed with both flexibility and security in mind, this system is perfect for managing library operations in a digital environment.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Setup Instructions](#setup-instructions)
- [Database Schema](#database-schema)
- [Technologies Used](#technologies-used)
- [API Endpoints](#api-endpoints)
  - [Authentication](#authentication)
  - [Author Management](#author-management)
  - [Book Management](#book-management)
  - [Combined Features](#combined-features)
- [Security Highlights](#security-highlights)
- [Future Enhancements](#future-enhancements)

---

## Overview

This Library Management System offers a RESTful API for managing users, books, and authors. Powered by **PHP** and **Slim Framework**, it ensures:

- Authentication and Authorization via JWT.
- Secure CRUD operations on entities.
- Logical relationships between books and authors.
- An extensible, maintainable architecture.

---

## Features

- **User Authentication**: 
  - Registration and Login via JWT-based authentication.
- **Books and Authors Management**:
  - Create, Read, Update, and Delete (CRUD) operations.
- **Secure Operations**:
  - Protect endpoints with token verification.
  - Data validation and duplicate checks.
- **Custom Endpoints**:
  - View authors with associated books.
  - Intuitive data representation for real-time library management.

---

## Setup Instructions

### Prerequisites
- PHP (7.4 or higher)
- Composer (Dependency Manager)
- MySQL Database
- A web browser and Postman for API testing

### Steps

1. Clone the repository:
   ```bash
   git clone [your-repository-url]
   cd [repository-name]
   ```

2. Install dependencies using Composer:
   ```bash
   composer install
   ```

3. Configure the database in your PHP file:
   ```php
   $servername = "localhost";
   $username = "root";
   $password = "";
   $dbname = "library";
   ```

4. Import the database schema (see [Database Schema](#database-schema)):
   ```bash
   mysql -u root -p library < schema.sql
   ```

5. Launch the local PHP server:
   ```bash
   php -S localhost:8000
   ```

6. Access the API using `http://localhost:8000`.

---

## Database Schema

```sql
CREATE TABLE users (
    userid INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) UNIQUE,
    password VARCHAR(255)
);

CREATE TABLE authors (
    authorid INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255)
);

CREATE TABLE books (
    bookid INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    authorid INT,
    FOREIGN KEY (authorid) REFERENCES authors(authorid)
);

CREATE TABLE books_authors (
    bookid INT,
    authorid INT,
    FOREIGN KEY (bookid) REFERENCES books(bookid),
    FOREIGN KEY (authorid) REFERENCES authors(authorid),
    PRIMARY KEY (bookid, authorid)
);
```

---

## Technologies Used

- **Backend Framework**: PHP (Slim Framework)
- **Database**: MySQL
- **Authentication**: JSON Web Tokens (JWT)
- **Libraries**: Firebase JWT, PSR-7 Implementation

---

## API Endpoints

### Authentication

- **Register User**: `POST /user/register`
- **Authenticate User**: `POST /user/auth`

### Author Management

- **Create Author**: `POST /user/author/create`
- **Read Authors**: `GET /user/author/read`
- **Update Author**: `PUT /user/author/update`
- **Delete Author**: `DELETE /user/author/delete`

### Book Management

- **Create Book**: `POST /user/book/create`
- **Read Books**: `GET /user/book/read`
- **Update Book**: `PUT /user/book/update`
- **Delete Book**: `DELETE /user/book/delete`

### Combined Features

- **Get Authors with Books**: `GET /books`

---

## Security Highlights

- Password hashing using SHA-256.
- Token verification for protected routes.
- Prepared statements to prevent SQL Injection.
- Token expiration enforced for added security.

---

## Future Enhancements

- Implement role-based access controls (e.g., admin, librarian).
- Add pagination for large datasets.
- Enhance API responses with detailed error messages.
- Create a user-friendly front-end interface.
- Integrate additional reporting features (e.g., borrowing history, popular authors).

---

Thank you for exploring this Library Management System! For issues, suggestions, or contributions, feel free to create a pull request or open an issue on the repository.
