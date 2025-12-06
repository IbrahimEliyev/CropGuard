# Customer Requirements Document (CRD)

**Project:** CropGuard - Plant Disease Risk Prediction System  
**Document ID:** CG-CRD-001  
**Version:** 1.0  
**Date:** 2025-12-04  
**Status:** Final Draft

---

## 1. Introduction and Project Context

### 1.1 Purpose

This Customer Requirements Document (CRD) defines the complete set of customer and stakeholder requirements for the **CropGuard Plant Disease Risk Prediction Web Application**.
It serves as the authoritative baseline for **scope validation**, **feature alignment**, and **acceptance testing** throughout the Software Development Life Cycle (SDLC).

### 1.2 Product Vision

CropGuard delivers a **responsive, intelligent, and data-driven platform** that enables farmers and agricultural professionals to **predict and prevent plant diseases** before they occur.
By integrating **advanced machine learning models** with **agronomic data** and **climate intelligence**, the application empowers users to make **proactive farming decisions** and reduce crop losses.

The platform aims to become the **most accessible and intelligent** web-based plant disease prediction service for modern agriculture, featuring **climate-aware risk assessment**, **location-based forecasting**, and **actionable recommendations** accessible from any device.

### 1.3 Target Audience

The primary users are farmers, agricultural professionals, and organizations involved in crop production and management.
Key user groups include:

- Small to medium-scale farmers
- Agricultural consultants and advisors
- Farm managers and plantation owners
- Agricultural research institutions
- Agribusinesses and cooperatives
- Extension workers and field agents
- General agricultural community seeking preventive crop management

---

## 2. Functional Requirements

Functional requirements are presented as **User Stories**, reflecting user goals and benefits.

| **ID**    | **Module**                  | **User Story**                                                                                                                                                                          |
| :-------- | :-------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **F-1.1** | Onboarding                  | As a New User, I want to register using my **email and password** so that I can securely access personalized disease prediction services.                                               |
| **F-1.2** | Authentication              | As a Returning User, I want to log in and log out securely so that my field data and predictions are protected.                                                                         |
| **F-1.3** | User Dashboard              | As a Farmer, I want a personalized dashboard showing my fields, recent predictions, and risk alerts so that I can monitor my crops at a glance.                                         |
| **F-2.1** | Field Management            | As a User, I want to create and manage multiple fields with details (location, crop type, soil type) so that I can track different areas separately.                                    |
| **F-2.2** | Location Selection          | As a User, I want to select my field location on an **interactive map** or by region so that climate data is accurate for my area.                                                      |
| **F-2.3** | Crop Information Input      | As a User, I want to enter **crop type, growth stage, planting date, and irrigation method** through a guided form so that predictions are tailored to my specific conditions.          |
| **F-3.1** | Disease Prediction          | As a User, I want to submit my field data and receive **predicted plant diseases with risk scores** so that I can prepare prevention measures in advance.                               |
| **F-3.2** | Climate Integration         | As a User, I want the system to automatically fetch **wind speed, humidity, temperature, season, and climate zone** for my location so that predictions consider environmental factors. |
| **F-3.3** | Risk Assessment             | As a User, I want to see a **color-coded risk level** (low, medium, high) for each predicted disease so that I can prioritize my actions.                                               |
| **F-3.4** | Disease Information         | As a User, I want to view **detailed descriptions of predicted diseases** including symptoms and prevention methods so that I understand what to look for.                               |
| **F-4.1** | Prediction History          | As a User, I want to access **historical predictions** for my fields so that I can track disease patterns over seasons.                                                                 |
| **F-4.2** | Field Comparison            | As a User, I want to **compare disease risks across multiple fields** so that I can allocate resources effectively.                                                                     |
| **F-4.3** | Recommendations             | As a User, I want to receive **personalized prevention recommendations** (e.g., "Apply fungicide within 3 days") based on predicted risks so that I can take timely action.             |
| **F-4.4** | Alert Notifications         | As a User, I want to receive **automated alerts** (email or in-app) when high-risk diseases are predicted for my fields so that I can respond immediately.                              |
| **F-5.1** | Interactive Map View        | As a User, I want to view my fields on an **interactive map with risk indicators** so that I can visualize geographic patterns.                                                         |
| **F-5.2** | Nearby Crop Tracking        | As a User, I want to specify **nearby crops** in the form so that predictions consider cross-contamination risks.                                                                       |
| **F-5.3** | Seasonal Insights           | As a User, I want to see **seasonal disease trends** for my region so that I can plan planting schedules better.                                                                        |
| **F-6.1** | Admin User Management       | As a System Administrator, I want to manage users, field data, and system logs so that I can ensure service quality and data integrity.                                                 |
| **F-6.2** | Model Maintenance           | As a System Administrator, I want to **retrain and redeploy** the prediction model periodically with new disease data so that accuracy improves over time.                              |
| **F-6.3** | Climate API Management      | As a System Administrator, I want to monitor climate API usage and switch backup sources if needed so that predictions remain reliable.                                                 |

---

## 3. Non-Functional Requirements

### 3.1 Performance

| **ID**  | **Requirement**        | **Description**                                                                                    |
| :------ | :--------------------- | :------------------------------------------------------------------------------------------------- |
| **P-1** | Prediction Response    | Disease prediction API responses shall not exceed **2.0 seconds** for standard requests.          |
| **P-2** | Page Load              | Initial page load time shall be under **3 seconds** on standard broadband connections.            |
| **P-3** | Scalability            | The system shall scale horizontally to support **5,000 concurrent active users**.                  |
| **P-4** | Climate Data Freshness | Climate data shall be cached and refreshed every **6 hours** to balance accuracy and performance. |

### 3.2 Security and Privacy

| **ID**  | **Requirement** | **Description**                                                                                                                   |
| :------ | :-------------- | :-------------------------------------------------------------------------------------------------------------------------------- |
| **S-1** | Authentication  | The system shall use **JWT-based session management** for secure login with salted password hashing (e.g., bcrypt).               |
| **S-2** | Encryption      | All communications shall be secured using **HTTPS (TLS 1.3)**; all secrets and API keys stored as **encrypted environment variables**. |
| **S-3** | Privacy Policy  | The system must ensure **field location data is encrypted** and accessible only to the owning user.                               |
| **S-4** | Access Control  | Admin features shall be restricted to authorized users via **role-based access control (RBAC)**.                                  |

### 3.3 Usability and Interface

| **ID**  | **Requirement**  | **Description**                                                                                                            |
| :------ | :--------------- | :------------------------------------------------------------------------------------------------------------------------- |
| **U-1** | Responsiveness   | The web app shall provide a **fully responsive design** across mobile, tablet, and desktop devices.                        |
| **U-2** | Accessibility    | The interface shall conform to **WCAG 2.1 Level AA** accessibility guidelines.                                             |
| **U-3** | Guided Flow      | The prediction form shall use a **step-by-step wizard interface** to simplify data entry.                                  |
| **U-4** | Map Integration  | Location selection shall use **interactive maps** (Leaflet.js or Mapbox) with field boundary drawing.                      |
| **U-5** | Visualization    | Risk levels and disease information shall be presented with **color-coded indicators and intuitive icons**.                |
| **U-6** | Theme            | The application shall support **dark and light themes**, switchable by user preference.                                    |

### 3.4 Technical Constraints

| **ID**  | **Constraint**         | **Description**                                                                                                                           |
| :------ | :--------------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| **T-1** | Backend Framework      | The backend must be developed in **Python (FastAPI)**, chosen for high performance and ML integration.                                    |
| **T-2** | Frontend Framework     | The frontend shall be built using **React** with **TailwindCSS** for modern, responsive UI.                                               |
| **T-3** | Database               | The system shall use **PostgreSQL** for structured storage and **Redis** for caching climate and prediction data.                         |
| **T-4** | ML Model Integration   | Disease prediction models must run server-side using **scikit-learn, TensorFlow, or PyTorch**, exposing inference endpoints via FastAPI. |
| **T-5** | Climate API Sources    | The system shall integrate **weather APIs** (e.g., OpenWeatherMap, WeatherAPI) with automatic failover if primary source fails.           |
| **T-6** | Prediction Accuracy    | The prediction model must maintain a minimum **accuracy ≥ 85%** and **F1-score ≥ 0.80** on validation datasets.                           |
| **T-7** | Mapping APIs           | Interactive maps shall use **Leaflet.js or Mapbox** integrated via the backend's geo-data pipeline.                                       |

---

## 4. Document Control

| **Version** | **Date**   | **Description**              | **Author**      |
| :---------- | :--------- | :--------------------------- | :-------------- |
| 1.0         | 2025-12-04 | Initial CropGuard CRD (Final Draft) | Project Analyst |

---

**End of Document**
