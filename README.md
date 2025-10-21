# 📞 Phonebook Application

A full-stack phonebook application that allows users to manage contacts with names and phone numbers. The application features a React frontend and an Express.js backend with MongoDB database integration.

## 🌐 Live Demo

This application is hosted on **[Render.com](https://render.com)**

## 🚀 Features

- ✅ Add new contacts with name and phone number
- ✅ View all contacts in a list
- ✅ Update existing contact phone numbers
- ✅ Delete contacts
- ✅ Phone number validation (format: XX-XXXXXX or XXX-XXXXXXX, minimum 8 digits)
- ✅ Name validation (minimum 3 characters)
- ✅ Real-time info page showing total contacts and server time
- ✅ Error handling with descriptive messages
- ✅ Morgan HTTP request logger
- ✅ MongoDB integration with Mongoose ODM

## 🛠️ Tech Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** (v5.1.0) - Web framework
- **MongoDB** - NoSQL database
- **Mongoose** (v8.16.2) - MongoDB object modeling
- **Morgan** (v1.10.0) - HTTP request logger
- **dotenv** (v17.2.0) - Environment variable management

### Frontend
- **React** - UI framework
- **Vite** - Build tool and dev server

### Development Tools
- **ESLint** (v9.31.0) - Code linting
- **@stylistic/eslint-plugin** - Code style enforcement
- **Node --watch** - Development auto-reload

## 📁 Project Structure

```
phonebook-backend/
├── dist/                      # Built React frontend files
│   ├── assets/               # Bundled JS and CSS files
│   ├── index.html            # Main HTML file
│   └── vite.svg              # Favicon
├── models/
│   └── person.js             # Mongoose Person schema and model
├── requests/                 # REST Client test files
│   ├── create_person.rest    # POST request examples
│   ├── delete_person.rest    # DELETE request examples
│   ├── get_all_persons.rest  # GET all persons
│   ├── get_one_person.rest   # GET single person
│   └── update_person.rest    # PUT request examples
├── .env                      # Environment variables (not in git)
├── .gitignore               # Git ignore rules
├── eslint.config.mjs        # ESLint configuration
├── index.js                 # Main Express server file
├── mongo.js                 # MongoDB connection utility script
├── package.json             # Node.js dependencies and scripts
└── README.md                # This file
```

## 📋 Prerequisites

Before running this application, make sure you have:

- **Node.js** (v14 or higher) installed
- **MongoDB Atlas** account (or local MongoDB instance)
- **npm** or **yarn** package manager

## ⚙️ Installation & Setup

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd phonebook-backend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in the root directory:

```env
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster-url>/<database>?retryWrites=true&w=majority
PORT=3001
```

Replace `<username>`, `<password>`, `<cluster-url>`, and `<database>` with your MongoDB Atlas credentials.

### 4. Run the Application

**Development mode (with auto-reload):**
```bash
npm run dev
```

**Production mode:**
```bash
npm start
```

The server will start on the port specified in your `.env` file (default: 3001).

### 5. Access the Application

- **Frontend**: `http://localhost:3001`
- **API Base URL**: `http://localhost:3001/api/persons`
- **Info Page**: `http://localhost:3001/info`

## 🔌 API Endpoints

### Base URL: `/api/persons`

| Method | Endpoint | Description | Request Body | Response |
|--------|----------|-------------|--------------|----------|
| **GET** | `/api/persons` | Get all persons | - | Array of person objects |
| **GET** | `/api/persons/:id` | Get a single person by ID | - | Person object or 404 |
| **POST** | `/api/persons` | Create a new person | `{ "name": "string", "number": "string" }` | Created person object |
| **PUT** | `/api/persons/:id` | Update a person's number | `{ "number": "string" }` | Updated person object |
| **DELETE** | `/api/persons/:id` | Delete a person | - | 204 No Content |
| **GET** | `/info` | Get phonebook info | - | HTML page with stats |

### Request/Response Examples

#### Create a Person
```http
POST /api/persons
Content-Type: application/json

{
  "name": "John Doe",
  "number": "123-4567890"
}
```

**Success Response (200):**
```json
{
  "id": "507f1f77bcf86cd799439011",
  "name": "John Doe",
  "number": "123-4567890"
}
```

#### Get All Persons
```http
GET /api/persons
```

**Success Response (200):**
```json
[
  {
    "id": "507f1f77bcf86cd799439011",
    "name": "John Doe",
    "number": "123-4567890"
  },
  {
    "id": "507f1f77bcf86cd799439012",
    "name": "Jane Smith",
    "number": "987-6543210"
  }
]
```

#### Update a Person
```http
PUT /api/persons/507f1f77bcf86cd799439011
Content-Type: application/json

{
  "number": "111-2223333"
}
```

**Success Response (200):**
```json
{
  "id": "507f1f77bcf86cd799439011",
  "name": "John Doe",
  "number": "111-2223333"
}
```

#### Delete a Person
```http
DELETE /api/persons/507f1f77bcf86cd799439011
```

**Success Response (204 No Content)**

### Error Responses

#### Validation Error (400)
```json
{
  "error": "Person validation failed: name: Path `name` is required."
}
```

#### Malformed ID (400)
```json
{
  "error": "malformatted id"
}
```

#### Not Found (404)
```json
{
  "error": "unknown endpoint"
}
```

## ✅ Data Validation

### Person Schema

- **name**: 
  - Type: String
  - Required: Yes
  - Minimum length: 3 characters

- **number**: 
  - Type: String
  - Required: Yes
  - Format: Must match pattern `XX-XXXXXX` or `XXX-XXXXXXX` (2-3 digits, hyphen, remaining digits)
  - Minimum length: 8 characters total
  - Example valid numbers: `09-1234556`, `040-22334455`, `123-4567890`

## 🧪 Testing API Endpoints

The `requests/` folder contains REST Client files for testing. If you're using VS Code, install the **REST Client** extension and open any `.rest` file to send requests directly.

## 🌍 Deploying to Render.com

### Step-by-Step Deployment Guide

#### 1. Prepare Your Repository

Make sure your code is pushed to a Git repository (GitHub, GitLab, or Bitbucket).

```bash
git add .
git commit -m "Prepare for deployment"
git push origin main
```

#### 2. Create a Render Account

1. Go to [https://render.com](https://render.com)
2. Sign up for a free account
3. You can sign up with GitHub for easier integration

#### 3. Create a New Web Service

1. Click **"New +"** button in the Render dashboard
2. Select **"Web Service"**
3. Connect your Git repository:
   - If using GitHub, authorize Render to access your repositories
   - Select your phonebook repository

#### 4. Configure Web Service Settings

Fill in the following details:

- **Name**: `phonebook-app` (or your preferred name)
- **Region**: Choose the closest region to your users
- **Branch**: `main` (or your default branch)
- **Root Directory**: Leave empty (or specify if your code is in a subdirectory)
- **Runtime**: `Node`
- **Build Command**: `npm install`
- **Start Command**: `npm start`
- **Instance Type**: Select **"Free"** for testing

#### 5. Add Environment Variables

In the "Environment Variables" section, click **"Add Environment Variable"** and add:

| Key | Value |
|-----|-------|
| `MONGODB_URI` | Your MongoDB Atlas connection string |
| `PORT` | (Leave empty - Render assigns this automatically) |

**Note**: Render automatically provides the `PORT` environment variable, so you don't need to set it manually.

Example `MONGODB_URI`:
```
mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/phonebook?retryWrites=true&w=majority
```

#### 6. Deploy

1. Click **"Create Web Service"**
2. Render will automatically:
   - Clone your repository
   - Install dependencies
   - Start your application
3. Monitor the deployment logs to ensure everything works correctly

#### 7. Access Your Deployed Application

Once deployment is complete, Render provides you with a URL like:
```
https://phonebook-app-xxxx.onrender.com
```

Your application will be accessible at this URL.

### Important Notes for Render Deployment

1. **Free Tier Limitations**:
   - Free instances spin down after 15 minutes of inactivity
   - First request after inactivity may take 30-60 seconds to respond
   - Consider upgrading to a paid plan for production use

2. **Automatic Deploys**:
   - Render automatically redeploys when you push to your connected branch
   - You can disable auto-deploy in settings if needed

3. **MongoDB Atlas Setup**:
   - Make sure MongoDB Atlas allows connections from anywhere (0.0.0.0/0) or add Render's IP addresses
   - In MongoDB Atlas: **Network Access** → **Add IP Address** → **Allow Access from Anywhere**

4. **Static Files**:
   - Your `dist/` folder contains the frontend build
   - Express serves it with `app.use(express.static('dist'))`
   - Make sure `dist/` is committed to your repository

5. **Environment Variables**:
   - Never commit `.env` file to Git
   - Always use Render's environment variables dashboard

### Troubleshooting Render Deployment

**Problem**: Application crashes on startup
- **Solution**: Check logs in Render dashboard, verify `MONGODB_URI` is correct

**Problem**: MongoDB connection fails
- **Solution**: Ensure MongoDB Atlas network access allows Render IPs (0.0.0.0/0)

**Problem**: 404 errors for frontend routes
- **Solution**: Ensure `dist/` folder is in your repository and committed

**Problem**: Port binding errors
- **Solution**: Make sure you're using `process.env.PORT` in your code (already configured in `index.js`)

## 🔧 Utility Scripts

### mongo.js

A utility script to interact with MongoDB directly:

```bash
node mongo.js <password>
```

This script connects to MongoDB and displays all persons in the phonebook.

## 📝 Development Scripts

```bash
npm start        # Start production server
npm run dev      # Start development server with auto-reload
npm run lint     # Run ESLint to check code quality
npm test         # Run tests (currently not configured)
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the ISC License.

## 👨‍💻 Author

Your Name

## 🙏 Acknowledgments

- Full Stack Open course by University of Helsinki
- MongoDB Atlas for database hosting
- Render.com for application hosting
- React and Express.js communities

---

**Happy Coding! 🚀**
