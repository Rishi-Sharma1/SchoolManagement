# School Management API

A RESTful API built with Node.js, Express, and MySQL to manage school data. It allows users to add new schools and retrieve a list of schools sorted by their geographical proximity to a specified location.

## Features

- **Add a School**: Stores school details including name, address, latitude, and longitude in a MySQL database.
- **List Schools**: Fetches all schools and sorts them based on their distance from the user's provided coordinates.
- **ES Modules**: Modern JavaScript syntax (`import`/`export`) used throughout the project.

## Technologies Used

- Node.js
- Express.js
- MySQL (with `mysql2` package)
- CORS
- Body-Parser
- Dotenv

## Prerequisites

- Node.js (v14 or higher recommended)
- MySQL Server installed and running

## Installation and Setup

1. **Clone the repository or download the source code:**

   ```bash
   git clone <repository-url>
   cd "Nodejs Assignment"
   ```

2. **Install dependencies:**

   ```bash
   npm install
   ```

3. **Set up the Database:**

   Create a MySQL database and a `schools` table using the following SQL commands:

   ```sql
   CREATE DATABASE school_management;

   USE school_management;

   CREATE TABLE schools (
     id INT AUTO_INCREMENT PRIMARY KEY,
     name VARCHAR(255) NOT NULL,
     address VARCHAR(255) NOT NULL,
     latitude FLOAT NOT NULL,
     longitude FLOAT NOT NULL
   );
   ```

4. **Environment Variables:**

   Create a `.env` file in the root directory and add your MySQL database credentials:

   ```env
   PORT=5000
   DB_HOST=localhost
   DB_USER=root
   DB_PASSWORD=your_password
   DB_NAME=school_management
   ```

5. **Start the Development Server:**

   ```bash
   npm run dev
   ```

   The server will start on `http://localhost:5000` (or the port specified in `.env`).

## API Endpoints

### 1. Add a School

- **Endpoint:** `POST /addSchool`
- **Description:** Adds a new school to the database.
- **Request Body (JSON):**

  ```json
  {
    "name": "Springfield High School",
    "address": "123 Main St, Springfield",
    "latitude": 39.7817,
    "longitude": -89.6501
  }
  ```

- **Success Response:**
  - **Code:** 201 Created
  - **Content:**
    ```json
    {
      "success": true,
      "message": "School added successfully",
      "schoolId": 1
    }
    ```

- **Error Responses:**
  - **Code:** 400 Bad Request (Missing fields or invalid data types)
  - **Code:** 500 Internal Server Error (Database errors)

### 2. List Schools

- **Endpoint:** `GET /listSchools`
- **Description:** Retrieves a list of all schools, sorted by distance from the provided user coordinates.
- **Query Parameters:**
  - `latitude` (required): The user's latitude.
  - `longitude` (required): The user's longitude.
- **Example Request:** `GET /listSchools?latitude=39.7800&longitude=-89.6500`
- **Success Response:**
  - **Code:** 200 OK
  - **Content:**
    ```json
    {
      "success": true,
      "count": 1,
      "data": [
        {
          "id": 1,
          "name": "Springfield High School",
          "address": "123 Main St, Springfield",
          "latitude": 39.7817,
          "longitude": -89.6501,
          "distance": "0.19"
        }
      ]
    }
    ```

- **Error Responses:**
  - **Code:** 400 Bad Request (Missing query parameters)
  - **Code:** 500 Internal Server Error (Database errors)

## Project Structure

```
├── config/
│   └── db.js            # MySQL database connection configuration
├── controllers/
│   └── schoolController.js  # Request handlers for endpoints
├── routes/
│   └── schoolRoutes.js  # Express router configuration
├── utils/
│   └── distance.js      # Utility function to calculate geographical distance
├── .env                 # Environment variables (not tracked by git)
├── package.json         # Project metadata and dependencies
├── server.js            # Application entry point
└── README.md            # Project documentation
```
