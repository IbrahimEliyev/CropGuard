# Software Requirements Specification (SRS)

**Project:** CropGuard - Plant Disease Risk Prediction System  
**Document ID:** CG-SRS-001  
**Version:** 1.0  
**Date:** 2025-12-04  
**Status:** Draft

---

## 1. Introduction

### 1.1 Purpose

This document defines the **software requirements** for CropGuard, including functional and non-functional specifications, system architecture, and data handling. It serves as the primary reference for developers, testers, and stakeholders during the SDLC.

### 1.2 Scope

CropGuard is a **responsive, intelligent web application** that provides:

- **Climate-aware plant disease risk prediction** using ML models
- **Location-based analysis** with automatic climate data fetching
- **Guided data entry** for crop and field information
- **Historical prediction tracking** and field management
- **Field comparison** and **interactive map visualization**
- **Automated alerts** based on predicted disease risks
- **Personalized prevention recommendations** for farmers

The web app will support **user authentication**, **role-based administration**, and integration with **weather APIs** and **ML inference engines**.

### 1.3 Definitions, Acronyms, and Abbreviations

| Term       | Definition                                      |
| ---------- | ----------------------------------------------- |
| ML         | Machine Learning                                |
| API        | Application Programming Interface               |
| UI         | User Interface                                  |
| JWT        | JSON Web Token                                  |
| RBAC       | Role-Based Access Control                       |
| Risk Score | Probability (0-100%) of disease occurrence      |
| Field      | A user-defined agricultural area for monitoring |

### 1.4 References

- CRD Document: `CG-CRD-001`
- FastAPI Documentation: [https://fastapi.tiangolo.com](https://fastapi.tiangolo.com)
- React + TailwindCSS Guidelines: [https://reactjs.org](https://reactjs.org), [https://tailwindcss.com](https://tailwindcss.com)
- Climate Data Sources: OpenWeatherMap, WeatherAPI, Visual Crossing

---

## 2. Overall Description

### 2.1 Product Perspective

CropGuard is a **standalone web application** with client-server architecture:

- **Frontend:** React + TailwindCSS
- **Backend:** FastAPI (Python) with ML inference endpoints
- **Database:** PostgreSQL (user, field, prediction data), Redis (caching climate data)
- **External APIs:** Weather/climate data providers

### 2.2 Product Functions

- User registration and login
- Field creation and management
- Guided form for crop/field data entry
- Location selection via interactive map
- Disease prediction with risk assessment
- Historical prediction tracking
- Field comparison tools
- Interactive field map with risk indicators
- Alerts and prevention recommendations
- Admin management of users, logs, and ML model

### 2.3 User Classes and Characteristics

| User Class   | Characteristics                   | Privileges                                                          |
| ------------ | --------------------------------- | ------------------------------------------------------------------- |
| Farmer       | Primary user, field-level access  | Dashboard, field management, predictions, alerts, recommendations   |
| Consultant   | Multi-field/client management     | Same as farmer + client field monitoring                            |
| Admin        | Technical/system administrator    | User management, logs, model retraining, API monitoring             |

### 2.4 Operating Environment

- Web browsers: Chrome, Firefox, Edge, Safari (latest versions)
- Devices: Desktop, tablet, mobile (fully responsive)
- Backend hosted on cloud platform with HTTPS support

### 2.5 Design & Implementation Constraints

- FastAPI backend with Python ML model integration
- React frontend with TailwindCSS styling
- PostgreSQL and Redis database usage
- Weather API redundancy: automatic failover if API downtime >30s
- Prediction model accuracy: **≥ 85% accuracy, F1-score ≥ 0.80**

---

## 3. Functional Requirements

| ID   | Module                   | Description                                                            |
| ---- | ------------------------ | ---------------------------------------------------------------------- |
| F-1  | User Authentication      | Registration, login, logout with email/password and JWT sessions       |
| F-2  | Dashboard                | Display user fields, recent predictions, and risk alerts               |
| F-3  | Field Management         | Create, edit, delete fields with crop and location details            |
| F-4  | Prediction Form          | Step-by-step wizard for entering agronomic data                        |
| F-5  | Location Selection       | Interactive map for field location input with coordinates              |
| F-6  | Climate Data Integration | Automatic fetching of wind, humidity, temperature, season, climate zone|
| F-7  | Disease Prediction       | ML-based risk prediction with disease list and probabilities           |
| F-8  | Prediction History       | View and filter past predictions by field and date                     |
| F-9  | Field Comparison         | Compare disease risks across multiple fields side-by-side              |
| F-10 | Interactive Field Map    | Map view showing all fields with color-coded risk indicators           |
| F-11 | Alerts                   | Threshold-based notifications via email/in-app for high-risk diseases  |
| F-12 | Recommendations          | Prevention advice based on predicted diseases and risk levels          |
| F-13 | Admin Panel              | User, log, API monitoring, and model management                        |

---

## 4. Non-Functional Requirements

### 4.1 Performance

- Prediction API latency ≤ 2 seconds
- Page load ≤ 3 seconds
- Climate data cached for 6 hours
- System scales up to 5,000 concurrent users

### 4.2 Security

- HTTPS/TLS encryption for all traffic
- Passwords hashed with bcrypt
- JWT session management
- RBAC for admin features
- Field location data encrypted at rest

### 4.3 Usability

- Fully responsive UI
- Dark/light theme support
- Accessible (WCAG 2.1 Level AA)
- Step-by-step guided form
- Interactive maps for location selection

### 4.4 Reliability & Availability

- System uptime 99.5% (excluding maintenance)
- Weather API failover within 30 seconds
- Database backup and replication

---

## 5. System Architecture

### 5.1 High-Level Architecture

```
[Frontend (React + Tailwind)] <--> [FastAPI Backend + ML Inference] <--> [PostgreSQL + Redis]
                                     |
                                     v
                              [Weather APIs (Primary + Backup)]
```

### 5.2 Data Flow

1. User enters field and crop data via guided form
2. User selects location on interactive map
3. Backend fetches climate data for location (wind, humidity, temp, season, zone)
4. Backend combines user data + climate features
5. ML model predicts disease risks and probabilities
6. Results cached in Redis
7. Frontend renders predictions with color-coded risk levels
8. Alerts triggered if high-risk diseases detected

---

## 6. Database Design (High-Level)

**Tables:**

- `users` (id, email, password_hash, preferences, created_at)
- `fields` (id, user_id, name, location_coords, crop_type, soil_type, planting_date, irrigation_method, nearby_crops, created_at)
- `predictions` (id, field_id, prediction_date, diseases_json, climate_data_json, created_at)
- `alerts` (id, user_id, field_id, disease_name, risk_score, notification_sent, created_at)
- `disease_info` (disease_name, description, symptoms, prevention_methods)

---

## 7. External Interface Requirements

### 7.1 User Interfaces

- Web dashboard (React, Tailwind)
- Guided prediction form (multi-step wizard)
- Maps (Leaflet.js/Mapbox)
- Risk visualization (color-coded indicators)

### 7.2 APIs

- Weather/climate API (primary & backup)
- ML model endpoints (FastAPI inference API)
- Email notification API

---

## 8. System Features and Use Cases

1. **User Registration/Login**: Secure access with JWT
2. **Field Management**: Create and manage multiple fields
3. **Prediction Workflow**: 
   - Enter crop/field data (crop type, growth stage, soil, planting date, irrigation, nearby crops)
   - Select location on map
   - Submit for prediction
   - View disease list with risk scores
4. **Historical Tracking**: View past predictions by field
5. **Field Comparison**: Compare risks across fields
6. **Map Visualization**: Interactive map with field risk indicators
7. **Alerts**: Automated notifications for high-risk diseases
8. **Recommendations**: Prevention guidance per disease
9. **Admin Management**: User, log, and model management

---

## 9. ML Model Specifications

### 9.1 Input Features

**User-Provided:**
- Crop type (categorical)
- Growth stage (categorical)
- Soil type (categorical)
- Planting date (date → days since planting)
- Irrigation method (categorical)
- Nearby crops (multi-select categorical)

**Auto-Fetched (Climate):**
- Wind speed (numerical)
- Humidity (numerical)
- Temperature (numerical)
- Season (categorical)
- Climate zone (categorical)

### 9.2 Output

- List of probable diseases
- Risk score (0-100%) per disease
- Confidence level

### 9.3 Model Requirements

- Minimum accuracy: 85%
- Minimum F1-score: 0.80
- Inference time: < 1 second
- Model format: Pickle/ONNX/TensorFlow SavedModel

---

## 10. Acceptance Criteria

- All functional modules operate as specified
- ML predictions meet accuracy thresholds
- System uptime ≥ 99.5%
- Responsive UI across all devices
- Alerts and notifications delivered reliably
- Climate API failover works within 30 seconds

---

## 11. Appendices

- Weather API documentation references
- ML model training and validation report
- UI wireframes and mockups
- Database schema diagram

---

**End of SRS Document**
