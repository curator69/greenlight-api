# Greenlight API 🎬

Greenlight API is a JSON-based RESTful API for managing movie information, inspired by the Open Movie Database API. This project is built with **Go** and uses **PostgreSQL** as the database for storing movie details, user authentication, and more.

## Features 🌟

- **Movie Management**: Create, update, delete, and fetch movie details.
- **User Registration and Authentication**: User registration, activation, and JWT-based authentication.
- **Permission-based Authorization**: Secure user access to resources based on their permissions.
- **Rate Limiting**: Implement rate limiting to prevent abuse.
- **Filtering, Sorting, and Pagination**: Powerful query support for movie listings.
- **Graceful Shutdown**: Ensure that the API shuts down gracefully when required.
- **Structured Logging**: Clear and structured logs for easier debugging and monitoring.

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
- [Database Migrations](#database-migrations)
- [Acknowledgments](#acknowledgments "Acknowledgments")

## Tech Stack ⚙️

- **Go**: The backend language used for building the API.
- **PostgreSQL**: The database for persisting movie and user information.
- **JWT**: Used for securing user authentication.
- **Docker**: For containerization and easy setup.

## Installation 🔧

### 1. Clone the Repository

```bash
git clone https://github.com/curator69/greenlight-api.git
cd greenlight-api
```

### 2. Install Dependencies

Make sure you have Go and PostgreSQL installed. Then run:

```bash
go mod download
```

### 3. Setup Environment Variables

Create a .env file in the root directory and add the following:

```bash
GREENLIGHT_DB_DSN="postgres://username:password@localhost/greenlight?sslmode=disable"
```

Replace username and password with your PostgreSQL credentials.

### 4. Run the Database Migrations

```bash
make db/migrations/up
```

### 5. Start the API Server

```bash
make build/api
./bin/api
```

## Usage 🚀

Once the API server is running, you can interact with it using tools like Postman or curl. Below are some sample API requests.

### Authentication

```bash
# Register a new user
curl -X POST {{APP_URL}}/users -d '{"name":"Alice Smith", "email":"alice@example.com", "password":"pa55word"}'

# Log in to get the JWT token
curl -X POST {{APP_URL}}/tokens/authentication -d '{"email":"alice@example.com", "password":"pa55word"}'
```

### Movie Management

```bash
# Fetch all movies
curl -H "Authorization: Bearer YOUR_JWT_TOKEN" {{APP_URL}}/movies

# Add a new movie
curl -X POST -H "Authorization: Bearer YOUR_JWT_TOKEN" -d '{"title": "Inception", "year": 2010, "runtime": "148 mins", "genres": ["action", "sci-fi"]}' {{APP_URL}}/movies
```

## API Endpoints 📄

### Public Endpoints

- **GET** `/v1/healthcheck`: Check the API status.
- **POST** `/v1/users`: Register a new user.
- **POST** `/v1/tokens/authentication`: Log in and receive a JWT token.

### Protected Endpoints (Require JWT Token)

- **GET** `/v1/movies`: Retrieve a list of all movies.
- **POST** `/v1/movies`: Create a new movie.
- **GET** `/v1/movies/:id`: Get details of a specific movie.
- **PATCH** `/v1/movies/:id`: Update an existing movie.
- **DELETE** `/v1/movies/:id`: Delete a specific movie.

## Database Migrations 📋

To manage database schema migrations, this project uses the migrate tool. You can apply or rollback migrations using the following commands:

```bash
# Run migrations
make db/migrations/up

# Rollback migrations
make db/migrations/down
```

## Acknowledgments

[Alex Edwards](https://www.alexedwards.net/) for the [Let&#39;s Go Futher book](https://lets-go-further.alexedwards.net/ "Let's Go Futher book"), which inspired the structure of this project.
