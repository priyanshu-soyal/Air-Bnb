# 🏠 Airbnb Clone - WonderLust

A full-featured property listing application like Airbnb web application built with the MERN stack (MongoDB, Express, EJS, Node.js). This project demonstrates property listing management, user authentication, image uploads, and review systems - perfect for learning full-stack web development.

## ✨ Features

- **Property Listings**: Full CRUD operations for creating, viewing, editing, and deleting listings
- **User Authentication**: Secure signup/login system using Passport.js with local strategy
- **Image Upload**: Seamless image upload and cloud storage integration with Cloudinary
- **Review System**: Users can add and delete reviews on listings
- **Authorization**: Owner-based permissions for editing/deleting listings and reviews
- **Session Management**: Persistent sessions stored in MongoDB with express-session
- **Flash Messages**: User-friendly success and error notifications
- **Responsive Design**: Clean, modern UI with custom CSS styling

## 🛠️ Tech Stack

**Backend:**

- Node.js - Runtime environment
- Express.js - Web application framework
- MongoDB - NoSQL database
- Mongoose - MongoDB object modeling

**Frontend:**

- EJS (Embedded JavaScript) - Templating engine
- ejs-mate - Layout support for EJS
- CSS - Custom styling

**Authentication & Security:**

- Passport.js - Authentication middleware
- passport-local - Local authentication strategy
- passport-local-mongoose - Mongoose plugin for Passport

**File Upload:**

- Multer - Multipart/form-data handling
- Cloudinary - Cloud-based image storage and management

**Session & State:**

- express-session - Session middleware
- connect-mongo - MongoDB session store
- connect-flash - Flash message middleware

**Validation:**

- Joi - Schema validation

## 🚀 Getting Started

### Prerequisites

- Node.js (v22.13.1 or higher)
- MongoDB Atlas account (or local MongoDB installation)
- Cloudinary account for image storage

### Installation

1. **Clone the repository**

```bash
git clone https://github.com/priyanshu-soyal/Air-Bnb.git
cd Air-Bnb
```

2. **Install dependencies**

```powershell
npm install
```

3. **Set up environment variables**

Create a `.env` file in the project root and add the following:

```env
ATLASDB_URL=your_mongodb_connection_string_here
SECRET=your_session_secret_key
CLOUD_NAME=your_cloudinary_cloud_name
CLOUD_API_KEY=your_cloudinary_api_key
CLOUD_API_SECRET=your_cloudinary_api_secret
NODE_ENV=development
```

> **⚠️ Important:** Never commit your `.env` file to version control!

4. **Initialize the database (optional)**

To seed the database with sample data:

```powershell
node initDB/initDB.js
```

5. **Start the application**

```powershell
node app.js
```

The application will be available at **http://localhost:8080/listings**

## 📝 Environment Variables

| Variable           | Description                                      | Required |
| ------------------ | ------------------------------------------------ | -------- |
| `ATLASDB_URL`      | MongoDB connection string (MongoDB Atlas)        | Yes      |
| `SECRET`           | Secret key for session encryption                | Yes      |
| `CLOUD_NAME`       | Cloudinary cloud name                            | Yes      |
| `CLOUD_API_KEY`    | Cloudinary API key                               | Yes      |
| `CLOUD_API_SECRET` | Cloudinary API secret                            | Yes      |
| `NODE_ENV`         | Environment mode (`development` or `production`) | No       |

### Example `.env` file:

```env
ATLASDB_URL=mongodb+srv://username:password@cluster.mongodb.net/airbnb?retryWrites=true&w=majority
SECRET=mysupersecretkey123456
CLOUD_NAME=mycloud
CLOUD_API_KEY=123456789012345
CLOUD_API_SECRET=abcdefghijklmnopqrstuvwxyz
NODE_ENV=development
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

## 🗂️ Project Structure

```
17-AIR-BNB/
├── Controllers/          # Business logic for routes
│   ├── listingsController.js
│   ├── reviewsController.js
│   └── userController.js
├── models/              # Mongoose schemas
│   ├── Listing.js
│   ├── Reviews.js
│   └── User.js
├── routes/              # Express route definitions
│   ├── listingsRoute.js
│   ├── reviewRoute.js
│   └── userRoute.js
├── views/               # EJS templates
│   ├── layouts/
│   ├── listings/
│   ├── users/
│   └── includes/
├── public/              # Static assets
│   ├── CSS/
│   └── JS/
├── initDB/              # Database seeding scripts
│   ├── data.js
│   └── initDB.js
├── utils/               # Utility functions
│   ├── ExpressError.js
│   └── wrapAsync.js
├── app.js               # Application entry point
├── cloudConfig.js       # Cloudinary configuration
├── joiSchema.js         # Validation schemas
├── Middelwares.js       # Custom middleware
└── package.json         # Project dependencies
```

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

---
