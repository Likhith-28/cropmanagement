# Crop Management Portal

A web application for managing crops and crop enquiries. Users can create an account, track their crops, view dashboard summaries, and check weather for a crop location. Admin users can review and reply to enquiries.

## Features

- User registration and login
- Dashboard with crop totals and growing/harvested summaries
- Create, update, and delete crops
- Weather lookup for a crop location
- Submit and review enquiries
- Admin enquiry replies
- Protected dashboard routes using JWT authentication

## Tech stack

- Frontend: React, Vite, React Router, Bootstrap, Axios
- Backend: Node.js, Express, Mongoose, MongoDB
- Authentication: bcryptjs password hashing and JSON Web Tokens
- Weather: OpenWeather API

## Requirements

- Node.js and npm
- A MongoDB database, such as a MongoDB Atlas cluster
- An OpenWeather API key for weather lookup

## Setup

### 1. Configure the backend

From the project root:

```bash
cd backend
npm install
```

Copy `.env.example` to `.env` and fill in your values:

```env
PORT=5001
MONGODB_URI=mongodb+srv://<database-user>:<url-encoded-password>@<cluster-host>/cropmanagement?retryWrites=true&w=majority
JWT_SECRET=<a-long-random-secret>
```

Use a MongoDB **database user** in the connection string, and allow your IP address in the Atlas Network Access settings. Keep `.env` private; it is ignored by Git.

Start the API:

```bash
node server.js
```

The backend listens on port `5001` by default. It waits for the MongoDB connection before starting.

### 2. Configure the frontend

For dashboard weather lookup, create `frontend/.env.local` and add your OpenWeather API key:

```env
VITE_OPENWEATHER_API_KEY=your-openweather-api-key
```

The key is used by the browser, so restrict it in your OpenWeather account to the APIs and domains you need. Do not commit `.env.local`.

In a second terminal, from the project root:

```bash
cd frontend
npm install
npm run dev
```

Open the local URL printed by Vite, usually `http://localhost:5173`.

The frontend currently sends API requests to `http://localhost:5001`. If you change the backend port or deploy the app, update the API URLs in the frontend accordingly.

## Admin access

Public registration creates regular user accounts. Admin access should be assigned only by an authorized administrator in the database; it cannot be selected in the registration form.

## Notes

- Passwords are hashed before they are stored.
- JWT tokens are stored in browser local storage and expire after one hour.
- Weather lookup requires `VITE_OPENWEATHER_API_KEY` in `frontend/.env.local`.
- `backend/.env.example` documents the required backend environment variables. Never commit your real `.env` file or API keys.
