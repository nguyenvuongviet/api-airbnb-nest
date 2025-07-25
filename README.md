# Airbnb-like Booking Platform Backend

A backend system for an Airbnb-like booking platform built with [NestJS](https://nestjs.com/) and [Prisma](https://www.prisma.io/). This project provides a robust API with features including user authentication, room booking, conflict checking, user history, admin dashboard, image upload, and booking statistics.

## Features

- **User Authentication**: Secure registration and login system, with Google OAuth support.
- **Room Booking**: Create, update, and cancel room bookings.
- **Conflict Checking**: Ensures no overlapping bookings for the same room.
- **User History**: Tracks user booking history.
- **Admin Dashboard**: Manages users, bookings, and system settings.
- **Image Upload**: Integrates with Cloudinary for managing and uploading room listing images.
- **Booking Statistics**: Provides analytics and insights for bookings.
- **Email Notifications**: Supports sending email notifications (e.g., booking confirmations).

## Prerequisites

Before running the project, ensure you have the following installed:

- **Node.js** (version 16 or higher)
- **npm** (version 8 or higher)
- **MySQL** (version 8 or higher, as the project uses MySQL)
- **Git** (to clone the repository)

## Getting Started

Follow these steps to set up and run the project locally.

### 1. Clone the Repository

```bash
git clone https://github.com/nguyenvuongviet/api-airbnb-nest.git
cd api-airbnb-nest
```

### 2. Install Dependencies

Install the required npm packages:

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in the root directory and configure the environment variables based on the template below:

```env
PORT=3069
DATABASE_URL="mysql://<username>:<password>@<host>:<port>/<database_name>"
ACCESS_TOKEN_SECRET="<access_token_secret>"
ACCESS_TOKEN_EXPIRES="1d"
REFRESH_TOKEN_SECRET="<refresh_token_secret>"
REFRESH_TOKEN_EXPIRES="7d"
SENDER_EMAIL="<sender_email_address>"
SENDER_PASSWORD="<email_app_password>"
GOOGLE_CLIENT_ID="<google_client_id>"
GOOGLE_CLIENT_SECRET="<google_client_secret>"
CLOUDINARY_NAME="<cloudinary_account_name>"
CLOUDINARY_API_KEY="<cloudinary_api_key>"
CLOUDINARY_API_SECRET="<cloudinary_api_secret>"
```

**Explanation of Environment Variables**:
- `PORT`: The port the API will run on (default is 3069).
- `DATABASE_URL`: Connection string for the MySQL database. Replace:
  - `<username>`: MySQL username (e.g., `root`).
  - `<password>`: MySQL password.
  - `<host>`: MySQL server address (e.g., `localhost`).
  - `<port>`: MySQL port (e.g., `3307`).
  - `<database_name>`: Database name (e.g., `db_airbnb`).
- `ACCESS_TOKEN_SECRET` and `REFRESH_TOKEN_SECRET`: Secret keys for JSON Web Tokens (JWT). Generate secure random strings using a command like `openssl rand -base64 32`.
- `ACCESS_TOKEN_EXPIRES` and `REFRESH_TOKEN_EXPIRES`: Token expiration times (1 day for access token, 7 days for refresh token).
- `SENDER_EMAIL`: Email address used for sending notifications (e.g., Gmail).
- `SENDER_PASSWORD`: App Password for the email service.
- `GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET`: Credentials from Google Cloud Console for Google OAuth login.
- `CLOUDINARY_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET`: Credentials from Cloudinary for image management.

### 4. Set Up the Database

Ensure MySQL is running on the host and port specified in `DATABASE_URL` (default: `localhost:3307`). Create the database if it does not exist:

```sql
CREATE DATABASE db_airbnb;
```

Run the following command to set up the database schema using Prisma:

```bash
npx prisma db pull
npx prisma generate
```

This command will create the database tables based on the Prisma schema.

### 5. Compile and Run the Project

You can run the project in different modes:

- **Development Mode**:
  ```bash
  npm run start
  ```

- **Watch Mode** (automatically restarts on code changes):
  ```bash
  npm run start:dev
  ```

- **Production Mode**:
  ```bash
  npm run start:prod
  ```

The API will be available at `http://localhost:3069`.

### 6. Using Swagger for API Documentation

The project integrates Swagger (OpenAPI) to provide an interactive API documentation interface. To access the API documentation:

1. Ensure the server is running (using `npm run start` or `npm run start:dev`).
2. Open a browser and navigate to:
   ```
   http://localhost:3069/api-docs
   ```
3. The Swagger interface will display a list of all API endpoints, including:
   - (./assets/api_1.png)
   - (./assets/api_2.png)
   - (./assets/api_3.png)
   - (./assets/api_4.png)

**Notes**:
- Some endpoints (e.g., `/admin/dashboard` or `/rooms`) require authentication. Use the `/auth/login` or `/auth/google` endpoint to obtain an access token, then add the token to the `Authorization` header in the format `Bearer <access_token>` in the Swagger interface.
- To upload images via the `/upload` endpoint, use Swagger's file upload feature and ensure the Cloudinary variables are correctly configured in the `.env` file.