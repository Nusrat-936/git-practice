# Secure File Hosting Web Application

A full-stack web application built for **COSC2956: Internet Tools**. The system allows users to register, log in, upload files, view all uploaded files on the Downloads page, access only their own files in the My Files dashboard, and delete only files they own.

## Features

- User registration with unique username and email
- Secure login with **hashed passwords** using bcrypt
- **JWT authentication** for protected API routes
- Token stored in **browser localStorage**
- File upload with validation
  - Supported formats: **.pdf** and **.mp4**
  - Maximum file size: **20 MB**
- File metadata stored in **MongoDB**
- Downloads page showing all uploaded files for authenticated users
- My Files dashboard showing only the current user's files
- Secure deletion so users can delete **only their own files**
- Frontend built with **HTML, CSS, and JavaScript**
- All frontend data fetched dynamically from backend APIs

## Folder Structure

```bash
secure-file-hosting-project/
│
├── backend/
│   ├── config/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── uploads/
│   ├── .env.example
│   ├── package.json
│   └── server.js
│
├── frontend/
│   ├── css/
│   ├── js/
│   ├── register.html
│   ├── login.html
│   ├── upload.html
│   ├── my-files.html
│   └── downloads.html
│
├── .gitignore
└── README.md
```

## Technologies Used

- **Frontend:** HTML, CSS, JavaScript
- **Backend:** Node.js, Express.js
- **Database:** MongoDB + Mongoose
- **Authentication:** JSON Web Token (JWT)
- **Password Hashing:** bcryptjs
- **File Upload Handling:** multer

## Setup Instructions

### 1. Clone the repository

```bash
git clone <your-github-repository-link>
cd secure-file-hosting-project/backend
```

### 2. Install dependencies

```bash
npm install
```

### 3. Create the environment file

Create a `.env` file inside the `backend` folder and copy the values from `.env.example`.

Example:

```env
PORT=5000
MONGODB_URI=mongodb://127.0.0.1:27017/secure_file_hosting
JWT_SECRET=replace_this_with_a_long_random_secret
```

### 4. Start MongoDB

Make sure your MongoDB server is running locally.

If using MongoDB Community Server:

```bash
mongod
```

### 5. Start the backend server

```bash
npm run dev
```

or

```bash
npm start
```

### 6. Open the application in your browser

Visit:

```bash
http://localhost:5000/login
```

You can also go directly to:
- `http://localhost:5000/register`
- `http://localhost:5000/upload`
- `http://localhost:5000/my-files`
- `http://localhost:5000/downloads`

## API Endpoints

### Authentication

#### `POST /api/register`
Registers a new user.

**Request Body:**
```json
{
  "username": "demo1",
  "email": "demo1@example.com",
  "password": "123456"
}
```

#### `POST /api/login`
Logs in a user and returns a token.

**Request Body:**
```json
{
  "email": "demo1@example.com",
  "password": "123456"
}
```

### Files

#### `POST /api/upload`
Uploads a file. Requires authentication.

**Form Data:**
- `file`: PDF or MP4 file

#### `GET /api/public-files`
Returns all uploaded files. Requires authentication.

#### `GET /api/my-files`
Returns only files uploaded by the current user. Requires authentication.

#### `GET /api/files/:id/download`
Downloads a selected file. Requires authentication.

#### `DELETE /api/files/:id`
Deletes a file owned by the logged-in user. Requires authentication.

## Database Design

### User Collection
Stores authentication information:
- `id`
- `username`
- `email`
- `hashed password`
- `created_at`

### File Collection
Stores file metadata:
- `id`
- `filename`
- `path`
- `size`
- `uploaded_by`
- `uploaded_at`

## Security and Validation

- Passwords are hashed before being stored in the database
- JWT tokens are verified on all protected routes
- Duplicate email registration is blocked
- Duplicate usernames are blocked
- File types are restricted to `.pdf` and `.mp4`
- File size is limited to 20 MB
- Filenames are sanitized before storage
- Users can delete only their own files
- Frontend never accesses the database or filesystem directly

## Demo Video Checklist

Use this order in the demo video:

1. Register the first user
2. Log in as the first user
3. Upload a file
4. Open Downloads and confirm the file appears
5. Register a second user
6. Log in as the second user
7. Open Downloads and confirm the first user’s file is visible
8. Upload a second file
9. Open Downloads and confirm both files are visible
10. Open My Files and delete a file
11. Return to Downloads and confirm the deleted file is gone

## Notes for Submission

- Push the full project to GitHub
- Include this README in the repository
- Record a demo video showing all required features
- Make sure MongoDB is running before starting the backend
