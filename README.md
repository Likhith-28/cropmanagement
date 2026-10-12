# Crop Management Portal

A React and Node.js application for managing crop records and agricultural enquiries. Users can register, sign in, track crops, view dashboard summaries, and check weather for a crop location. Admin accounts can review and reply to enquiries.

## Features

- Register and log in with email and password
- Add, edit, and delete crop records
- View crop totals and growing/harvested summaries
- View weather for a crop's location
- Submit enquiries and review enquiry replies
- Protect dashboard pages with JWT authentication

## Technology

- Frontend: React, Vite, React Router, Bootstrap, Axios
- Backend: Node.js, Express, Mongoose
- Database: MongoDB
- Authentication: bcryptjs and JSON Web Tokens
- Weather: OpenWeather API

## Requirements

- Node.js and npm
- A MongoDB database, such as MongoDB Atlas
- An OpenWeather API key for weather lookup

## Run locally

### Backend

From the project root, install the backend dependencies:

```bash
cd backend
npm install
```

Create `backend/.env` with your own settings:

```env
PORT=5001
MONGODB_URI=mongodb+srv://<database-user>:<url-encoded-password>@<cluster-host>/cropmanagement?retryWrites=true&w=majority
JWT_SECRET=<a-long-random-secret>
```

Use your MongoDB **database user** credentials in the URI. In Atlas, allow your current IP address under Network Access. Keep the real `.env` file private and do not commit it.

Start the backend:

```bash
node server.js
```

The API uses port `5001` by default and starts after it connects to MongoDB.

### Frontend

Open a second terminal from the project root:

```bash
cd frontend
npm install
npm run dev
```

Open the local URL printed by Vite, usually `http://localhost:5173`.

The frontend currently sends API requests to `http://localhost:5001`. If you use a different backend port or deploy the application, update the frontend API URLs.

## Accounts and roles

Public registration creates a regular user account. Admin access must be assigned by an authorized administrator; it is not selectable on the registration form.

## Weather setup

The dashboard uses OpenWeather to retrieve current weather for a crop location. The API key is currently set in `frontend/src/pages/Dashboard.jsx`. Replace it with your own key, and restrict the key in your OpenWeather account. Do not publish a working API key in a public repository.

## Security

- Passwords are hashed before being stored.
- Login tokens expire after one hour and are stored in browser local storage.
- Never upload real database credentials, JWT secrets, or API keys.
