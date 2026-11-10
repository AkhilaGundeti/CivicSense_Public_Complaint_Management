# 🏛️ CivicSense - Public Complaint Management System

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-ISC-green.svg)
![Node](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen.svg)
![React](https://img.shields.io/badge/react-19.2.0-blue.svg)

**An intelligent, scalable complaint management platform that uses AI/NLP to automatically route public complaints to the correct government authorities.**

[Features](#-key-features) • [Installation](#-installation) • [Documentation](#-api-documentation) • [Architecture](#-architecture)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Special Features](#-special-features)
- [Tech Stack](#-tech-stack)
- [Architecture](#-architecture)
- [Installation](#-installation)
- [User Roles](#-user-roles)
- [API Documentation](#-api-documentation)
- [Project Structure](#-project-structure)
- [Future Improvements](#-future-improvements)

---

## 🎯 Overview

**CivicSense** is a full-stack MERN (MongoDB, Express, React, Node.js) application designed to revolutionize public complaint management in India. The system leverages cutting-edge AI and Natural Language Processing (NLP) to automatically analyze, categorize, prioritize, and route citizen complaints to the appropriate government authorities.

### Problem Statement

Traditional complaint management systems suffer from:
- Manual categorization leading to misrouting
- Inefficient priority assignment
- Lack of transparency for citizens
- No intelligent analysis of complaint content
- Limited support for anonymous reporting

### Solution

CivicSense addresses these challenges by:
- **Intelligent Urgency Scoring**: Multi-factor urgency calculation based on sentiment, keywords, and trust scores
- **Automatic Authority Assignment**: Routes complaints to the correct department (Water Board, IEB, RDA, etc.)
- **Anonymous/Semi-Anonymous Support**: Secure identity handling with optional reveal mechanisms
- **Real-time Analytics**: Comprehensive dashboards for authorities and administrators

---

## ✨ Key Features

### 👥 For Citizens

- **📝 Complaint Submission**
  - Submit complaints with description, location, and optional photos
  - Support for both logged-in and anonymous submissions
  - Real-time category detection and validation
  - Image upload support for visual evidence

- **🔒 Privacy & Anonymity**
  - Submit complaints anonymously (requires login)
  - Identity reveal system for anonymous complaints
  - Control over personal information visibility
  - Secure data handling

- **📊 Personal Dashboard**
  - View all submitted complaints
  - Track complaint status in real-time
  - View authority notes and updates
  - Complaint history and analytics

- **🏘️ Community Features**
  - Join location-based communities
  - View community announcements
  - Upvote local issues to increase priority
  - Community feed with local complaints

### 🏢 For Authorities

- **📋 Complaint Management**
  - View only complaints assigned to their department
  - Filter by status, urgency, and date
  - Update complaint status (pending → seen → in-progress → resolved)
  - Add notes and updates to complaints

- **🔍 Identity Management (FR2)**
  - Request identity reveal for anonymous complaints
  - View revealed citizen information when approved
  - Track identity request status
  - Secure identity handling

- **📈 Analytics Dashboard**
  - Overview statistics (total, pending, resolved)
  - Category-wise breakdown
  - Urgency distribution
  - Location-based trends
  - Performance metrics

- **💬 Communication**
  - Add notes to complaints
  - Request citizen contact information
  - Track communication history

### 👨‍💼 For Administrators

- **👥 User Management**
  - Create and manage authority accounts
  - Assign roles and departments
  - Monitor user activity

- **📊 System Analytics**
  - Comprehensive system-wide statistics
  - Category distribution analysis
  - Urgency trends over time
  - Location heatmaps
  - User engagement metrics

- **📥 Data Import**
  - Bulk CSV complaint upload
  - Automated processing and categorization
  - Data validation and error handling

- **🏘️ Community Management**
  - Create and manage communities
  - Publish announcements
  - Monitor community engagement
  - Issue tracking and management

---

## 🚀 Special Features

### 1. 🤖 NLP Pipeline

**Zero-Shot Classification**
- Uses HuggingFace's `DeBERTa-v3-base-mnli-fever-anli` model
- Automatically classifies complaints into 6 categories:
  - Water Issue
  - Electricity Issue
  - Road Issue
  - Garbage Issue
  - Safety Hazard
  - Environmental Issue
- No training data required - works out of the box
- Confidence scoring for classification reliability

**Sentiment Analysis**
- Uses `bert-base-multilingual-uncased-sentiment` model
- Analyzes complaint tone and emotional content
- Provides sentiment score (0-1) for urgency calculation
- Supports multiple languages

**Hybrid Urgency Detection**
- **Primary Logic**: Rule-based urgency scoring using:
  - Hazard keyword detection (weighted by severity)
  - Sentiment analysis scores
  - Trust scores (anonymous vs registered users)
  - Category confidence
- **AI Validation**: Optional AI enhancement for edge cases
- **Multi-factor Formula**:
  ```
  urgencyScore = (sentimentScore × 0.3) + 
                 (categoryConfidence × 0.2) + 
                 (hazardKeywordScore × 0.4) + 
                 (trustScore × 0.1)
  ```
- **Urgency Levels**: Critical (≥0.9), Urgent (≥0.7), Normal (<0.7)

**Key Phrase Extraction**
- Automatically extracts important keywords from complaints
- Used for search and categorization
- Improves complaint discoverability


### 2. 🔐 Anonymous/Semi-Anonymous Handling (FR2)

**Comprehensive Privacy System**

**Rule A: Anonymous Only When Logged In**
- Anonymous mode requires user authentication
- Prevents abuse and ensures accountability
- Maintains system integrity

**Rule B: Category-Based Identity Requirements**
- Certain categories require identification:
  - Water Issue
  - Electricity Issue
- Non-logged users cannot submit these categories
- Ensures proper service delivery

**Rule C: Personal Premises Detection**
- Automatically detects personal premises complaints
- Keywords: "my house", "inside home", "bathroom", etc.
- Requires login for personal property issues
- Prevents misuse of public complaint system

**Rule D: Category Override**
- If user selects anonymous but category requires identity:
  - System automatically disables anonymous mode
  - Informs user with clear message
  - Ensures compliance with category requirements

**Identity Request System**
- Authorities can request identity reveal for anonymous complaints
- Citizens receive notification and can approve/decline
- One-time reveal per complaint (not system-wide)
- Secure identity storage with selective visibility
- Audit trail for identity requests

**Trust Score System**
- Anonymous complaints: 0.3 trust score
- Registered complaints: 0.8 trust score
- Affects urgency calculation
- Encourages user registration while supporting privacy

### 3. 🎯 Automatic Authority Assignment

**Intelligent Routing**
- Maps complaint categories to appropriate authorities:
  - Water Issue → Water Board
  - Electricity Issue → IEB (Indian Electricity Board)
  - Road Issue → RDA (Road Development Authority)
  - Garbage Issue → Municipal Council
  - Safety Hazard → Police Safety
  - Environmental Issue → Municipal Council
  - Disaster/Flood/Storm → Disaster Management

**Benefits**
- Reduces manual routing errors
- Ensures complaints reach correct department
- Faster response times
- Improved accountability

### 4. 📊 Advanced Analytics & Statistics

**Overview Statistics**
- Total complaints count
- Status breakdown (pending, in-progress, resolved)
- Anonymous vs registered ratio
- Urgency distribution

**Category Analytics**
- Complaints per category
- Category-wise resolution rates
- Trend analysis over time

**Location Analytics**
- Geographic distribution of complaints
- Location-based trends
- Hotspot identification

**Temporal Analysis**
- Complaints over time (daily, weekly, monthly)
- Resolution time trends
- Peak complaint periods

### 5. 🏘️ Community Module

**Community Features**
- Location-based community creation
- Join/leave communities
- Community-specific announcements
- Local issue tracking

**Engagement Tools**
- Upvote system for local issues
- Community feed with announcements and complaints
- Member statistics
- Active issue tracking

**Admin Community Hub**
- Separate admin interface for community management
- Create/edit/delete announcements
- Monitor community engagement
- Issue management tools

### 6. 📥 CSV Bulk Import

**Features**
- Admin-only CSV upload functionality
- Automated processing of bulk complaints
- Field mapping: text, location, timestamp
- Automatic categorization and urgency scoring
- Error handling and validation
- Support for historical data import

### 7. 🔒 Security Features

**Authentication & Authorization**
- JWT-based authentication
- Role-based access control (RBAC)
- Protected routes and endpoints
- Secure password hashing (bcrypt)

**API Security**
- Rate limiting (100 requests per 15 minutes)
- Helmet.js for HTTP headers
- CORS configuration
- Input validation and sanitization

**Data Protection**
- Secure identity storage
- Anonymous complaint privacy
- Selective data visibility
- Audit logging

---

## 🛠️ Tech Stack

### Frontend
- **React 19.2.0** - UI library
- **Vite 7.2.2** - Build tool and dev server
- **React Router 6.26.0** - Client-side routing
- **Tailwind CSS 3.4.4** - Utility-first CSS framework
- **React Hook Form 7.52.0** - Form management
- **Axios 1.7.2** - HTTP client
- **Recharts 2.12.0** - Data visualization
- **React Leaflet 4.2.1** - Maps integration
- **Lucide React** - Icon library
- **AOS** - Scroll animations
- **React Hot Toast** - Notifications

### Backend
- **Node.js** - Runtime environment
- **Express.js 4.18.2** - Web framework
- **MongoDB** - NoSQL database
- **Mongoose 8.0.3** - ODM for MongoDB
- **JWT (jsonwebtoken)** - Authentication
- **Bcryptjs 2.4.3** - Password hashing
- **Multer 1.4.5** - File upload handling
- **Helmet 7.1.0** - Security middleware
- **Express Rate Limit** - Rate limiting
- **CSV Parser** - CSV processing
- **Dotenv** - Environment variables

### AI/NLP
- **@huggingface/inference 4.13.3** - Official HuggingFace client
- **HuggingFace Inference API** - Cloud-based NLP models
  - Sentiment Analysis: `nlptown/bert-base-multilingual-uncased-sentiment`
  - Zero-Shot Classification: `MoritzLaurer/DeBERTa-v3-base-mnli-fever-anli`

### Development Tools
- **Nodemon** - Auto-restart for development
- **ESLint** - Code linting
- **PostCSS & Autoprefixer** - CSS processing

---

## 🏗️ Architecture

### System Architecture

```
┌─────────────────┐
│   React Client  │
│   (Frontend)    │
└────────┬────────┘
         │ HTTP/REST
         │
┌────────▼────────┐
│  Express Server │
│   (Backend)     │
└────────┬────────┘
         │
    ┌────┴────┐
    │         │
┌───▼───┐ ┌──▼──────────┐
│MongoDB│ │ HuggingFace  │
│       │ │  Inference   │
│       │ │     API      │
└───────┘ └──────────────┘
```

### Backend Architecture (MVC Pattern)

```
server/
├── src/
│   ├── config/          # Configuration files
│   │   ├── database.js  # MongoDB connection
│   │   └── constants.js # App constants
│   │
│   ├── controllers/     # Request handlers
│   │   ├── complaintController.js
│   │   ├── authorityController.js
│   │   ├── citizenController.js
│   │   ├── adminController.js
│   │   └── statsController.js
│   │
│   ├── models/          # Mongoose schemas
│   │   ├── Complaint.js
│   │   ├── Citizen.js
│   │   ├── Authority.js
│   │   └── Admin.js
│   │
│   ├── routes/          # API routes
│   │   ├── complaintRoutes.js
│   │   ├── authorityRoutes.js
│   │   ├── citizenRoutes.js
│   │   ├── adminRoutes.js
│   │   └── statsRoutes.js
│   │
│   ├── services/        # Business logic
│   │   ├── nlpService.js        # AI/NLP processing
│   │   ├── urgencyService.js    # Urgency calculation
│   │   ├── authorityService.js   # Authority assignment
│   │   └── csvService.js        # CSV processing
│   │
│   ├── middleware/      # Express middleware
│   │   ├── auth.js      # JWT authentication
│   │   ├── role.js      # Role-based access
│   │   └── upload.js    # File upload handling
│   │
│   └── utils/           # Utility functions
│       ├── jwt.js       # JWT helpers
│       └── textProcessing.js # Text analysis
│
└── uploads/            # File storage
    ├── images/         # Complaint images
    └── csv/            # CSV uploads
```

### Frontend Architecture

```
client/
├── src/
│   ├── api/            # API client
│   │   ├── api.js      # API endpoints
│   │   └── axiosClient.js # Axios configuration
│   │
│   ├── components/     # Reusable components
│   │   ├── community/  # Community components
│   │   ├── ui/         # UI components
│   │   └── ...
│   │
│   ├── context/        # React Context
│   │   ├── AuthContext.jsx
│   │   └── CommunityContext.jsx
│   │
│   ├── pages/          # Page components
│   │   ├── citizen/    # Citizen pages
│   │   ├── authority/  # Authority pages
│   │   ├── admin/      # Admin pages
│   │   └── community/  # Community pages
│   │
│   ├── utils/          # Utilities
│   │   ├── constants.js
│   │   └── validations.js
│   │
│   └── layouts/        # Layout components
│       └── DashboardLayout.jsx
```

### Data Flow

1. **Complaint Submission**
   ```
   User → Frontend Form → Backend API → NLP Processing → 
   Category Detection → Urgency Calculation → Authority Assignment → 
   Database Storage → Response
   ```

2. **NLP Processing Pipeline**
   ```
   Description Text → Sentiment Analysis (Parallel) → Category Classification
                     ↓                                    ↓
              Sentiment Score                    Category + Confidence
                     ↓                                    ↓
                     └──────────→ Urgency Calculation ←──┘
                                        ↓
                              Urgency Score + Level
   ```

3. **Identity Request Flow (FR2)**
   ```
   Authority → Request Identity → Notification to Citizen → 
   Citizen Approves/Declines → Identity Revealed/Denied → 
   Authority View Updated
   ```

---

## 📦 Installation

### Prerequisites

- **Node.js** ≥ 18.0.0
- **MongoDB** ≥ 5.0.0 (local or cloud instance)
- **npm** or **yarn**
- **HuggingFace API Key** (free tier available)

### Step 1: Clone Repository

```bash
git clone <repository-url>
cd JH
```

### Step 2: Backend Setup

```bash
cd server
npm install
```

Create `.env` file in `server/` directory:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# Database
MONGODB_URI=mongodb://localhost:27017/civicsense

# JWT Secret
JWT_SECRET=your-super-secret-jwt-key-change-in-production

# HuggingFace API
HUGGINGFACE_API_KEY=your-huggingface-api-key

# Client URL (for CORS)
CLIENT_URL=http://localhost:5173
```

### Step 3: Frontend Setup

```bash
cd ../client
npm install
```

Create `.env` file in `client/` directory (optional):

```env
VITE_API_URL=http://localhost:5000/api
```

### Step 4: Database Setup

Ensure MongoDB is running:

```bash
# Start MongoDB (if installed locally)
mongod
```

Or use MongoDB Atlas (cloud) and update `MONGODB_URI` in `.env`.

### Step 5: Seed Admin User (Optional)

```bash
cd server
npm run seed:admin
```

Default admin credentials:
- Email: `admin@civicsense.gov`
- Password: `admin123` (change in production!)

### Step 6: Run Application

**Terminal 1 - Backend:**
```bash
cd server
npm run dev
```

**Terminal 2 - Frontend:**
```bash
cd client
npm run dev
```

### Step 7: Access Application

- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:5000
- **API Docs**: http://localhost:5000/api
- **Health Check**: http://localhost:5000/health

---

## 👥 User Roles

### 1. Citizen 👤

**Capabilities:**
- Register and login
- Submit complaints (anonymous or identified)
- View personal complaint history
- Track complaint status
- Join communities
- Upvote local issues
- Approve/decline identity requests

**Access:**
- Public complaint submission (no login required)
- Anonymous submission (login required)
- Personal dashboard (login required)
- Community features (login required)

### 2. Authority 🏢

**Capabilities:**
- Login to authority portal
- View assigned complaints only
- Update complaint status
- Add notes and updates
- Request identity for anonymous complaints
- View analytics dashboard
- Filter and search complaints

**Access:**
- Authority-specific dashboard
- Assigned complaints only (filtered by department)
- Statistics and analytics
- Identity request system

**Departments:**
- Water Board
- IEB (Indian Electricity Board)
- RDA (Road Development Authority)
- Municipal Council
- Police Safety
- Disaster Management

### 3. Administrator 👨‍💼

**Capabilities:**
- Full system access
- Create and manage authority accounts
- View all complaints system-wide
- Upload CSV files for bulk import
- Access comprehensive analytics
- Manage communities
- Create announcements
- Monitor system health

**Access:**
- Admin dashboard
- User management
- System analytics
- CSV upload
- Community management

---

## 📚 API Documentation

### Base URL
```
http://localhost:5000/api
```

### Authentication
Most endpoints require JWT authentication. Include token in header:
```
Authorization: Bearer <token>
```

### Citizen Endpoints

#### Register
```http
POST /api/citizens/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "+94771234567",
  "password": "password123"
}
```

#### Login
```http
POST /api/citizens/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "password123"
}
```

#### Get Profile
```http
GET /api/citizens/me
Authorization: Bearer <token>
```

### Complaint Endpoints

#### Submit Complaint
```http
POST /api/complaints
Content-Type: multipart/form-data

{
  "description": "Water leak in main street",
  "location": "Main Street, City",
  "category": "water issue",  // Optional, auto-detected if not provided
  "anonymous": "false",        // "true" or "false"
  "image": <file>              // Optional image file
}
```

**Response:**
```json
{
  "success": true,
  "message": "Complaint submitted successfully",
  "data": {
    "complaint": {
      "_id": "...",
      "description": "...",
      "category": "water issue",
      "urgencyScore": 0.75,
      "urgencyLevel": "urgent",
      "assignedAuthority": "water_board",
      "status": "pending",
      ...
    }
  }
}
```

#### Get My Complaints
```http
GET /api/complaints/my-complaints
Authorization: Bearer <token>
```

#### Get Complaint by ID
```http
GET /api/complaints/:id
Authorization: Bearer <token>
```

#### Request Identity (Authority Only)
```http
POST /api/complaints/:id/request-identity
Authorization: Bearer <token>
```

#### Approve Identity (Citizen Only)
```http
POST /api/complaints/:id/approve-identity
Authorization: Bearer <token>
```

#### Decline Identity (Citizen Only)
```http
POST /api/complaints/:id/decline-identity
Authorization: Bearer <token>
```

### Authority Endpoints

#### Login
```http
POST /api/authority/login
Content-Type: application/json

{
  "email": "authority@department.gov",
  "password": "password123"
}
```

#### Get Assigned Complaints
```http
GET /api/authority/complaints?status=pending&urgency=urgent&page=1&limit=10
Authorization: Bearer <token>
```

#### Update Complaint Status
```http
PATCH /api/authority/complaints/:id/status
Authorization: Bearer <token>
Content-Type: application/json

{
  "status": "in_progress"  // pending, seen, in_progress, resolved
}
```

#### Add Note
```http
POST /api/authority/complaints/:id/notes
Authorization: Bearer <token>
Content-Type: application/json

{
  "content": "Inspected the site, work in progress"
}
```

### Admin Endpoints

#### Login
```http
POST /api/admin/login
Content-Type: application/json

{
  "email": "admin@civicsense.gov",
  "password": "admin123"
}
```

#### Create Authority User
```http
POST /api/admin/authority-users
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "Jane Smith",
  "email": "jane@waterboard.gov",
  "password": "password123",
  "role": "water_board",
  "department": "Water Department"
}
```

#### Upload CSV
```http
POST /api/admin/upload-csv
Authorization: Bearer <token>
Content-Type: multipart/form-data

{
  "csv": <file>
}
```

**CSV Format:**
```csv
text,location,timestamp
"Water leak in main street","Main Street, City","2024-01-15T10:30:00"
"Power outage in sector 5","Sector 5, Downtown","2024-01-15T11:00:00"
```

### Statistics Endpoints

#### Overview Statistics
```http
GET /api/stats/overview
Authorization: Bearer <token>
```

#### Category Statistics
```http
GET /api/stats/category
Authorization: Bearer <token>
```

#### Urgent Complaints
```http
GET /api/stats/urgent
Authorization: Bearer <token>
```

#### Location Statistics
```http
GET /api/stats/location
Authorization: Bearer <token>
```

#### Trends Over Time
```http
GET /api/stats/trends?period=month
Authorization: Bearer <token>
```

---

## 📁 Project Structure

```
JH/
├── client/                 # React frontend
│   ├── src/
│   │   ├── api/           # API client configuration
│   │   ├── components/    # Reusable React components
│   │   ├── context/       # React Context providers
│   │   ├── pages/         # Page components
│   │   ├── utils/         # Utility functions
│   │   └── layouts/       # Layout components
│   ├── public/            # Static assets
│   └── package.json
│
├── server/                # Express backend
│   ├── src/
│   │   ├── config/        # Configuration files
│   │   ├── controllers/   # Request handlers
│   │   ├── models/        # Mongoose schemas
│   │   ├── routes/        # API routes
│   │   ├── services/      # Business logic
│   │   ├── middleware/    # Express middleware
│   │   └── utils/         # Utility functions
│   ├── uploads/           # File uploads
│   └── package.json
│
├── README.md              # This file
├── COMMUNITY_MODULE_README.md
└── ADMIN_COMMUNITY_HUB.md
```

---

## 🔮 Future Improvements

### Phase 1: Performance & Scalability (0-3 months)
- [ ] Redis caching for frequently accessed data
- [ ] CDN integration for static assets
- [ ] Cloud storage for images (AWS S3/Cloudinary)
- [ ] Database query optimization
- [ ] Connection pooling

### Phase 2: Advanced Features (3-6 months)
- [ ] Real-time updates with WebSockets
- [ ] Push notifications (Firebase/OneSignal)
- [ ] Mobile applications (React Native)
- [ ] SMS/Email notifications
- [ ] WhatsApp integration
- [ ] Multi-language support (Sinhala, Tamil)

### Phase 3: AI Enhancements (6-12 months)
- [ ] Fine-tuned models for Indian context
- [ ] Image analysis for complaint photos
- [ ] Duplicate complaint detection
- [ ] Predictive analytics for resolution time
- [ ] Automated response suggestions
- [ ] Location-based clustering

### Phase 4: Integration & Expansion (12+ months)
- [ ] Government system APIs integration
- [ ] Social media integration
- [ ] Public API for third-party developers
- [ ] Regional expansion (South Asia)
- [ ] Open-source community contributions

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the ISC License.

---

## 👨‍💻 Authors

- **Development Team** - *Initial work*

---

## 🙏 Acknowledgments

- HuggingFace for providing excellent NLP models
- MongoDB for robust database solutions
- React and Express.js communities
- All contributors and testers

---

## 📞 Support

For support, email support@civicsense.gov or open an issue in the repository.

---

<div align="center">

**Built with ❤️ for better public service in India**

[⬆ Back to Top](#-civicsense-public-complaint-management-system)

</div>
