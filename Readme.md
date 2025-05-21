# Vehicle Parking Management System

## Table of Contents
1. [Introduction](#introduction)  
2. [Module Overview](#module-overview)  
3. [Architecture Overview](#architecture-overview)  
4. [Module-Wise Design](#module-wise-design)  
5. [Deployment Strategy](#deployment-strategy)  
6. [Database Design](#database-design)  
7. [User Interface Design](#user-interface-design)  
8. [Non-Functional Requirements](#non-functional-requirements)  
9. [Assumptions and Constraints](#assumptions-and-constraints)  
10. [Folder Structure](#folder-structure)  

---

## 1. Introduction
This document outlines the Low-Level Design (LLD) for a **Vehicle Parking Management System** that facilitates efficient parking slot management, vehicle entry/exit logging, reservations, and billing operations. The system aims to streamline both visitor and subscriber parking operations in real time.  

The backend is developed using **Spring Boot** with **JPA** and **MySQL**, while the frontend is built using **ReactJS**.

---

## 2. Module Overview
### 2.1 User Management
- Handles registration, login, and role-based access for admins, staff, and customers.

### 2.2 Parking Slot Management
- Manages slot types, occupancy status, and availability.

### 2.3 Vehicle Entry & Exit Logging
- Tracks vehicle movement and updates slot status.

### 2.4 Reservation System
- Enables users to book slots in advance and manage them.

### 2.5 Billing and Payments
- Generates bills based on usage duration and allows payment processing.

---

## 3. Architecture Overview
### 3.1 Architectural Style
- **Frontend**: ReactJS  
- **Backend**: REST API-based (Spring Boot)  
- **Database**: Relational (MySQL)  

### 3.2 Component Interaction
- Frontend communicates with backend APIs.  
- Backend manages business logic and data operations.  
- Database stores persistent data like user info, reservations, and invoices.  

---

## 4. Module-Wise Design
### 4.1 User Management Module
**Features**  
- Register and login  
- Assign roles and permissions  

**Entities**  
- `User`: UserID, Name, Email, Phone, Role, Password (hashed)  

### 4.2 Parking Slot Management Module
**Features**  
- Add/remove/update parking slots  
- Check real-time availability  

**Entities**  
- `ParkingSlot`: SlotID, Type (2W/4W), IsOccupied, Location  

### 4.3 Vehicle Entry & Exit Logging Module
**Features**  
- Log entry and exit  
- Calculate duration and update occupancy  

**Entities**  
- `VehicleLog`: LogID, VehicleNumber, EntryTime, ExitTime, SlotID, UserID  

### 4.4 Reservation System Module
**Features**  
- View availability and reserve slots  
- Modify or cancel reservations  

**Entities**  
- `Reservation`: ReservationID, UserID, SlotID, VehicleNumber, StartTime, EndTime, Status  

### 4.5 Billing and Payments Module
**Features**  
- Dynamic billing based on time and vehicle type  
- Payment via multiple modes  

**Entities**  
- `Invoice`: InvoiceID, UserID, Amount, PaymentMethod, Status, Timestamp  

---

## 5. Deployment Strategy
### 5.1 Local Development
- Frontend served via React dev server.  
- Backend run with Spring Boot.  
- Database setup using local MySQL instance.  

---

## 6. Database Design
| Table Name   | Primary Key   | Foreign Keys         |  
|--------------|---------------|----------------------|  
| User         | UserID        | –                    |  
| ParkingSlot  | SlotID        | –                    |  
| VehicleLog   | LogID         | UserID, SlotID       |  
| Reservation  | ReservationID | UserID, SlotID       |  
| Invoice      | InvoiceID     | UserID               |  

---

## 7. User Interface Design
### 7.1 Wireframe Elements
- Login/Signup  
- Dashboard for Admin/Staff/User  
- Slot Availability Map  
- Reservation Page  
- Vehicle Entry/Exit Management  
- Billing Summary and Payment  

---

## 8. Non-Functional Requirements
### 8.1 Performance
- Support 200+ concurrent users in dev/test setups.  

### 8.2 Scalability
- Horizontal scalability using containerization (optional in future).  

### 8.3 Security
- Role-based access.  
- Encrypted password storage.  
- HTTPS for all data exchange.  

### 8.4 Usability
- Responsive and mobile-friendly UI.  
- WCAG-compliant design.  

---

## 9. Assumptions and Constraints
### Assumptions
- Each slot can accommodate only one vehicle.  
- Entry/exit operations are manual or via scanner.  

### Constraints
- SMS/Email notification is out of scope.  
- Third-party integrations are not included in this phase.  

---

## 10. Folder Structure
```
vehicle-parking-management-system

├── eureka-discovery-service

│   ├── src

│   │   ├── main

│   │   │   ├── java

│   │   │   │   └── com

│   │   │   │       └── parking

│   │   │   │           └── discovery

│   │   │   │               └── EurekaDiscoveryServiceApplication.java

│   │   │   └── resources

│   │   │       ├── application.properties

│   │   │       └── bootstrap.yml

│   ├── pom.xml

│   └── README.md

├── api-gateway

│   ├── src

│   │   ├── main

│   │   │   ├── java

│   │   │   │   └── com

│   │   │   │       └── parking

│   │   │   │           └── gateway

│   │   │   │               └── ApiGatewayApplication.java

│   │   │   └── resources

│   │   │       ├── application.properties

│   │   │       └── bootstrap.yml

│   ├── pom.xml

│   └── README.md

├── user-service

│   ├── src

│   │   ├── main

│   │   │   ├── java

│   │   │   │   └── com

│   │   │   │       └── parking

│   │   │   │           └── user

│   │   │   │               ├── controllers

│   │   │   │               │   └── UserController.java

│   │   │   │               ├── entities

│   │   │   │               │   └── User.java

│   │   │   │               ├── repositories

│   │   │   │               │   └── UserRepository.java

│   │   │   │               ├── services

│   │   │   │               │   └── UserService.java

│   │   │   │               └── dtos

│   │   │   │                   └── UserDTO.java

│   │   │   └── resources

│   │   │       ├── application.properties

│   │   │       └── bootstrap.yml

│   ├── pom.xml

│   └── README.md

├── parking-slot-service

│   ├── src

│   │   ├── main

│   │   │   ├── java

│   │   │   │   └── com

│   │   │   │       └── parking

│   │   │   │           └── slot

│   │   │   │               ├── controllers

│   │   │   │               │   └── ParkingSlotController.java

│   │   │   │               ├── entities

│   │   │   │               │   └── ParkingSlot.java

│   │   │   │               ├── repositories

│   │   │   │               │   └── ParkingSlotRepository.java

│   │   │   │               ├── services

│   │   │   │               │   └── ParkingSlotService.java

│   │   │   │               └── dtos

│   │   │   │                   └── ParkingSlotDTO.java

│   │   │   └── resources

│   │   │       ├── application.properties

│   │   │       └── bootstrap.yml

│   ├── pom.xml

│   └── README.md

├── vehicle-log-service

│   ├── src

│   │   ├── main

│   │   │   ├── java

│   │   │   │   └── com

│   │   │   │       └── parking

│   │   │   │           └── log

│   │   │   │               ├── controllers

│   │   │   │               │   └── VehicleLogController.java

│   │   │   │               ├── entities

│   │   │   │               │   └── VehicleLog.java

│   │   │   │               ├── repositories

│   │   │   │               │   └── VehicleLogRepository.java

│   │   │   │               ├── services

│   │   │   │               │   └── VehicleLogService.java

│   │   │   │               └── dtos

│   │   │   │                   └── VehicleLogDTO.java

│   │   │   └── resources

│   │   │       ├── application.properties

│   │   │       └── bootstrap.yml

│   ├── pom.xml

│   └── README.md

├── reservation-service

│   ├── src

│   │   ├── main

│   │   │   ├── java

│   │   │   │   └── com

│   │   │   │       └── parking

│   │   │   │           └── reservation

│   │   │   │               ├── controllers

│   │   │   │               │   └── ReservationController.java

│   │   │   │               ├── entities

│   │   │   │               │   └── Reservation.java

│   │   │   │               ├── repositories

│   │   │   │               │   └── ReservationRepository.java

│   │   │   │               ├── services

│   │   │   │               │   └── ReservationService.java

│   │   │   │               └── dtos

│   │   │   │                   └── ReservationDTO.java

│   │   │   └── resources

│   │   │       ├── application.properties

│   │   │       └── bootstrap.yml

│   ├── pom.xml

│   └── README.md

├── billing-service

│   ├── src

│   │   ├── main

│   │   │   ├── java

│   │   │   │   └── com

│   │   │   │       └── parking

│   │   │   │           └── billing

│   │   │   │               ├── controllers

│   │   │   │               │   └── BillingController.java

│   │   │   │               ├── entities

│   │   │   │               │   └── Invoice.java

│   │   │   │               ├── repositories

│   │   │   │               │   └── InvoiceRepository.java

│   │   │   │               ├── services

│   │   │   │               │   └── BillingService.java

│   │   │   │               └── dtos

│   │   │   │                   └── InvoiceDTO.java

│   │   │   └── resources

│   │   │       ├── application.properties

│   │   │       └── bootstrap.yml

│   ├── pom.xml

│   └── README.md

└── README.md
 
```

---  