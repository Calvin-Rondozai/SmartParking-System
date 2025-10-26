<<<<<<< HEAD
## SmartParking – Project Overview

### Architecture

- **Mobile app (React Native)**: User auth, availability, booking, cancel, history.
- **Admin dashboard (HTML/CSS/JS)**: Dashboard, devices, bookings, users, reports, settings (dark mode). Superadmin can write; staff is read-only.
- **Backend (Django + DRF)**: REST API for auth, bookings, lots/spots, reports, IoT.
- **IoT (ESP32)**: Sends telemetry to backend; LEDs reflect slot status: Blue=booked, Green=empty, Red=occupied.

### Backend

- Apps: `parking_app`, `iot_integration`.
- Key models: `ParkingLot`, `ParkingSpot`, `Booking`, `UserProfile`, `IoTDevice`, `SensorData`, `DeviceLog`.
- Key views: auth, bookings CRUD, availability, `dashboard_reports`, `user_statistics`, IoT `register_device`, `sensor_data`, device details.
- Auth: Token-based (header `Authorization: Token <token>`). Dashboard permissions: superadmin write; staff read-only; general users no access.

### Admin Dashboard

- Location: `admin_dashboard/` → `index.html`, `styles.css`, `script.js`.
- Sections: Dashboard, Lots, Devices, Bookings, Users, Alerts, Reports, Settings.
- Core behaviors: client-side routing, manual refresh buttons (no auto-refresh churn), dark mode persisted in `localStorage`.
- Bookings: Filters (status/slot/date), CSV export, view/delete actions, slot labels normalized to “Slot A/B”.
- Users: Search (name/email), sort, CSV export, view; delete available to superadmin.

### Mobile App

- Location: `frontend/`.
- Uses fetch/axios to call DRF with stored token. Basic flow: login → view availability → book/cancel → view history.

### IoT Integration

- ESP32 posts to `iot_integration` endpoints. Backend maps telemetry to `ParkingSpot` and drives LED colors (booked=blue, empty=green, occupied=red).

### Common Endpoints (adjust to your `urls.py`)

- Auth: `POST /api/auth/login/`
- Bookings: `GET /api/admin/bookings/`, `DELETE /api/admin/bookings/{id}/`
- Spots/Lots: `GET /api/parking/spots/`
- Reports: `GET /api/dashboard_reports/`, `GET /api/user_statistics/`
- IoT: `POST /api/iot/register_device/`, `POST /api/iot/sensor_data/`, `GET /api/iot/device/details/`

### Running Locally

- Backend:
  - `cd backend`
  - `python manage.py migrate`
  - `python manage.py runserver 8000`
- Admin dashboard:
  - Open `admin_dashboard/index.html` in a browser (or serve statically).
  - Set admin token in console: `localStorage.setItem('adminToken','YOUR_TOKEN')`.
- Mobile app:
  - `cd frontend`
  - `npm install` or `yarn`
  - Configure backend base URL in services
  - `npx react-native run-android` or `run-ios`

### Notes

- If API endpoints differ, update `apiBaseUrl` and `iotApiUrl` in `admin_dashboard/script.js`.
- Staff users will see read-only actions on dashboard resources.
=======
# SmartParking-System
SmartParking System is an IoT-enabled solution with a React Native app, Django backend, admin dashboard, and ESP32 sensors. It offers real-time parking monitoring, booking, automated billing, overtime detection, AI-powered occupancy and revenue predictions, notifications, and wallet management.

# SmartParking System

**SmartParking System** is an IoT-enabled smart parking solution integrating a React Native mobile app, Django backend, admin dashboard, and ESP32 sensors. It provides real-time parking monitoring, booking management, automated billing, overtime detection, and AI-powered occupancy & revenue predictions.

---

## Table of Contents
- [Features](#features)
- [System Architecture](#system-architecture)
- [Technology Stack](#technology-stack)
- [Installation](#installation)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
- [IoT Hardware](#iot-hardware)
- [License](#license)

---

## Features
- Real-time parking spot monitoring
- Booking, extend, and cancellation system
- Overtime detection and automated billing
- AI-powered occupancy forecasting and revenue predictions
- Wallet management and push notifications
- Admin dashboard for user and device management
- WhatsApp chatbot integration for support

---

## System Architecture

### Backend (Django + DRF)
- **Database:** SQLite (development), PostgreSQL (production)
- **Authentication:** Token-based
- **Apps:** 
  - `parking_app`: Core parking functionality
  - `iot_integration`: ESP32 device management
  - `ai_analytics`: Machine learning predictions
  - `chatbot`: WhatsApp integration

### Mobile App (React Native + Expo)
- User authentication and profile management
- Real-time parking availability and booking
- Wallet and notification system
- Chatbot integration

### Admin Dashboard
- Real-time metrics, charts, occupancy grid
- Booking and user management
- AI insights and reports
- Device monitoring

### IoT Hardware (ESP32)
- Ultrasonic sensors for occupancy detection
- RGB LEDs for visual status (Red=Occupied, Green=Empty, Blue=Booked)
- IR sensor and buzzer for alerts
- WiFi communication to backend

---

## Technology Stack
- **Backend:** Django 4.2, Django REST Framework, Celery, Pandas, NumPy, Scikit-learn
- **Frontend (Mobile):** React Native, Expo SDK 53, React Navigation v7, Axios
- **Admin Dashboard:** JavaScript, CSS3, HTML5, Chart.js
- **IoT:** ESP32, Arduino IDE, HC-SR04 sensors, RGB LEDs

---

## Installation

### Backend
```bash
cd backend
python -m venv venv
source venv/bin/activate   # Linux/Mac
venv\Scripts\activate      # Windows
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
Frontend
bash
Copy code
cd frontend
npm install
expo start
Usage
Open the mobile app to register/login

View available parking spots

Book, extend, or cancel bookings

Monitor bookings and wallet balance

Admins can manage users, bookings, devices, and view AI insights

API Endpoints
Authentication
swift
Copy code
POST /api/auth/signup/ - Register
POST /api/auth/signin/ - Login
GET /api/auth/profile/ - Get profile
PUT /api/auth/profile/update/ - Update profile
Parking Management
bash
Copy code
GET /api/parking-lots/ - List lots
GET /api/parking-spots/ - List spots
POST /api/bookings/ - Create booking
GET /api/bookings/ - List user bookings
PUT /api/bookings/{id}/cancel/ - Cancel booking
IoT
swift
Copy code
POST /api/iot/devices/register/ - Register device
POST /api/iot/sensor/data/ - Send sensor data
GET /api/iot/parking/availability/ - Real-time availability
GET /api/iot/bookings/active/ - Active bookings for LED control
AI Analytics
swift
Copy code
GET /api/ai/occupancy/ - Occupancy predictions
GET /api/ai/revenue/ - Revenue predictions
GET /api/ai/user-behavior/ - User behavior analysis
IoT Hardware Configuration
Ultrasonic Sensors: Detect car presence

RGB LEDs: Visual indicator for each slot

IR Sensor & Buzzer: Alerts

ESP32 Pin Mapping: Configured per slot for sensors and LEDs
>>>>>>> e1346d4c15007e7a3d73e491af9733c7769a2dbf
