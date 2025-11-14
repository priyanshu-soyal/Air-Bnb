# Airbnb Clone

A small, educational Airbnb-like web application built with Node.js, Express and MongoDB. It allows users to sign up, list properties, upload images (Cloudinary), and create reviews. The app was built as part of a full-stack course project and is designed to be simple, readable, and easy to extend.

## Highlights

- CRUD for Listings (create, read, update, delete)
- User authentication with Passport (local strategy)
- Image upload and storage using Cloudinary
- Reviews tied to listings (deletes cascade when a listing is removed)
- Flash messages and session storage using MongoDB (connect-mongo)

## Tech stack

- Node.js (Express)
- MongoDB (Mongoose)
- EJS + ejs-mate for server-side rendering
- Passport for authentication
- Cloudinary for image storage
- Multer for multipart/form-data upload handling

## Quick start

1. Clone the repository

2. Install dependencies

```powershell
npm install
```

3. Create a `.env` file in the project root (see Environment variables below)

4. Run the app

```powershell
node app.js
# or use nodemon if you have it installed
```

By default the app listens on port 8080. Open http://localhost:8080/listings in your browser.

## Environment variables

Create a `.env` file (or set environment variables) with the following keys:

- ATLASDB_URL - MongoDB connection string (MongoDB Atlas recommended)
- SECRET - Session secret for express-session
- CLOUD_NAME - Cloudinary cloud name
- CLOUD_API_KEY - Cloudinary API key
- CLOUD_API_SECRET - Cloudinary API secret
- NODE_ENV - set to `production` in a production environment (optional)

Example `.env` (do NOT commit this file):

```
ATLASDB_URL=your_mongodb_connection_string_here
SECRET=some_long_random_secret
CLOUD_NAME=your_cloudinary_name
CLOUD_API_KEY=your_key
CLOUD_API_SECRET=your_secret
```

## Database seeding / init

There is an `initDB` folder (`initDB/initDB.js` and `initDB/data.js`) included in the project. You can inspect and run that file to seed the database with sample data. Make sure `ATLASDB_URL` is set before running.

## Important routes

- Listings

  - GET /listings — list all listings (home for listings)
  - GET /listings/new — form to create a new listing (requires login)
  - POST /listings — create a new listing (image upload to Cloudinary)
  - GET /listings/:id — view a single listing and its reviews
  - GET /listings/:id/edit — edit a listing (requires owner)
  - PUT /listings/:id — update a listing (image upload allowed)
  - DELETE /listings/:id — delete a listing

- Reviews

  - POST /listings/:id/reviews — add a review to a listing (requires login)
  - DELETE /listings/:id/reviews/:reviewId — delete a review (requires authorization)

- Users
  - GET /signup, POST /signup — register a new user
  - GET /login, POST /login — login
  - GET /logout — logout

See the `routes` folder for the exact implementation and middleware usage.

## Project structure (top-level)

- `app.js` — application entry point and server configuration
- `Controllers/` — controller logic for listings, reviews, and users
- `models/` — Mongoose models (Listing, Reviews, User)
- `routes/` — Express routers for the app's endpoints
- `views/` — EJS templates and layouts
- `public/` — static assets (CSS, client JS)
- `cloudConfig.js` — Cloudinary configuration and Multer storage
- `initDB/` — optional seeding scripts
- `uploads/` — (if present) local images (Cloudinary is used by default)

## Notes & assumptions

- The app expects Cloudinary for image uploads (configured in `cloudConfig.js`). If you prefer local storage, modify the multer configuration.
- Sessions are stored in MongoDB via `connect-mongo`. Be sure `ATLASDB_URL` and `SECRET` are set.
- There is no `start` script in `package.json`. You can add one if you want to run with `npm start`.

## To improve or extend

- Add tests and a simple test runner (e.g., Jest + Supertest for routes).
- Add a `start` and `dev` script to `package.json` (e.g., `nodemon app.js`).
- Harden security headers (helmet), rate limiting, and input sanitization.
- Add API endpoints if you want a JSON API in addition to server-rendered pages.

## Contributing

Feel free to open a PR or issue. Keep changes small and focused. Add tests where applicable.

## License

This repository is provided for learning/demo purposes. Check with the original project source or instructor for license details.
