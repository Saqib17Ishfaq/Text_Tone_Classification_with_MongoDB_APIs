Text Tone Classification API with MongoDB
https://img.shields.io/badge/Python-3.8%252B-blue,
https://img.shields.io/badge/Flask-2.0%252B-green,
https://img.shields.io/badge/MongoDB-5.0%252B-brightgreen,
https://img.shields.io/badge/PyTorch-1.10%252B-orange,
https://img.shields.io/badge/HuggingFace-Transformers-yellow

A comprehensive REST API for text tone classification using RoBERTa model with MongoDB integration, user authentication, and admin features.

Table of Contents:
      Features/n
      Technologies Used/n
      API Endpoints/n
      Setup Instructions/n
      Authentication/n
      Usage Examples
      Database Schema
      Error Handling
      Security
      Deployment
      Troubleshooting
      Future Enhancements

Features:
      Text Tone Analysis: Classifies text into multiple emotional tones using RoBERTa model
      User Authentication: JWT-based secure authentication system
      Role-Based Access Control: Admin and user roles with different permissions
      Password Security: Strong password validation and bcrypt hashing
      MongoDB Integration: Persistent storage for user data and analysis results
      Comprehensive API: Well-documented endpoints for all functionality
      Error Handling: Detailed error responses for all scenarios

Technologies Used:
      Backend: Python, Flask
      Database: MongoDB Atlas
      NLP Model: RoBERTa for sequence classification
      Authentication: JWT (JSON Web Tokens)
      Password Hashing: bcrypt
      Dependencies:
      PyTorch
      Transformers (HuggingFace)
      Flask-CORS
      PyMongo

API Endpoints:
      Authentication
      Endpoint	Method	Description	Auth Required
      /signup	POST	Register new user	No
      /signin	POST	User login	No
      /change-password	POST	Change user password	Yes
      Text Analysis
      Endpoint	Method	Description	Auth Required
      /analyze	POST	Analyze text tone	Yes
      User Management (Admin Only)
      Endpoint	Method	Description	Auth Required
      /users	GET	Get all users or specific user	Yes (Admin)
      /token	GET	Generate test token (dev only)	No
      python app.py
      The server will start on http://localhost:5000

Setup Instructions:
      Prerequisites
      Python 3.8+
      MongoDB Atlas account or local MongoDB instance
      PyTorch compatible with your hardware (CUDA if available)

Authentication:
      Signup Requirements
      Password must:
      Be exactly 8 characters long
      Contain at least one uppercase letter
      Contain at least one lowercase letter
      Contain at least one number
      Contain at least one special character

JWT Tokens
      Tokens are valid for 24 hours
      Include user role for authorization
      Must be sent in the Authorization header as:
      text
      Authorization: Bearer <token>

Usage Examples:
      User Registration
      curl -X POST http://localhost:5000/signup \
        -H "Content-Type: application/json" \
        -d '{
          "username": "newuser",
          "email": "user@example.com",
          "password": "Pass@123"
        }'
      User Login
      curl -X POST http://localhost:5000/signin \
        -H "Content-Type: application/json" \
        -d '{
          "login": "newuser",
          "password": "Pass@123"
        }'
      Text Analysis
      curl -X POST http://localhost:5000/analyze \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer <your_token>" \
        -d '{
          "text": "I am extremely happy with this wonderful product!"
        }'
      Admin Access to User Data
      curl -X GET http://localhost:5000/users \
        -H "Authorization: Bearer <admin_token>"
      Database Schema
      Users Collection
      javascript
      {
        "username": String,        // Unique identifier
        "email": String,           // Unique email
        "password": String,        // Hashed password
        "role": String,            // "admin" or "user"
        "created_at": DateTime,    // Account creation timestamp
        "phone": String,           // Optional
        // ... other optional fields
      }
      Text Analysis Collection
      javascript
      {
        "UserID": String,          // Reference to user
        "Text": String,            // Analyzed text
        "Timestamp": DateTime,     // Analysis time
        "DominantTone": {
          "tone": String,          // Highest confidence tone
          "confidence": Number     // Percentage confidence
        }
        
Error Handling:
      The API returns consistent error responses with:
      HTTP status code
      Error message
      Error details (when applicable)
      Status code in response body

Example error response:
      json
      {
        "error": "Invalid credentials",
        "status": 401
      }
      Security
      Password Storage: bcrypt hashing with salt
      Data Transmission: HTTPS recommended in production
      Authentication: JWT with expiration
      Input Validation: For all endpoints
      Role-Based Access Control: For sensitive operations

Deployment:
      For production deployment:
      Set up a proper WSGI server (Gunicorn, uWSGI)
      Configure Nginx/Apache as reverse proxy
      Set proper CORS policies
      Use HTTPS with valid certificate
      Rotate the secret key
      Implement rate limiting

Example Gunicorn command:
    gunicorn -w 4 -b 0.0.0.0:5000 app:app
    Troubleshooting

Common Issues:
    MongoDB Connection Failed:
    Verify connection string
    Check network access to MongoDB Atlas
    Ensure IP is whitelisted in Atlas
    Model Loading Errors:
    Verify model path is correct
    Check file permissions
    Ensure all model files are present

Authentication Issues:
    Verify token is included in Authorization header
    Check token expiration
    Ensure secret key matches

Future Enhancements
    Add more tone categories
    Implement batch text processing
    Add user profile management
    Include tone analysis history per user
    Implement API rate limiting
    Add Swagger/OpenAPI documentation
    Dockerize the application
    Add unit and integration tests
