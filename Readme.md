# Vehicle Parking Management System

## Introduction
This document outlines the Low-Level Design (LLD) for a **Vehicle Parking Management System** that facilitates efficient parking slot management, vehicle entry/exit logging, reservations, and billing operations. The system aims to streamline both visitor and subscriber parking operations in real time. The backend is developed using **Spring Boot**, **JPA**, and **MySQL**.

## Architecture Overview

### 1. Architectural Style
- **Frontend**: React, HTML, CSS.
- **Backend**:  Spring Boot application.
- **Database**: Relational database (MySQL).

### 2. Component Interaction
- The frontend communicates with backend APIs.
- The backend handles business logic and data operations.
- The database stores persistent data such as user information, reservations, and invoices.

### 3. Deployment Strategy
- **Local Development**:
    - Frontend served via Angular CLI or React dev server.
    - Backend run with Spring Boot.
    - Database setup using a local MySQL instance.

### 4. Folder Structure
```
vehicle-parking-management-system
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── parking
│   │   │           ├── controllers
│   │   │           │   ├── UserController.java
│   │   │           │   ├── ParkingSlotController.java
│   │   │           │   ├── VehicleLogController.java
│   │   │           │   ├── ReservationController.java
│   │   │           │   └── BillingController.java
│   │   │           ├── entities
│   │   │           │   ├── User.java
│   │   │           │   ├── ParkingSlot.java
│   │   │           │   ├── VehicleLog.java
│   │   │           │   ├── Reservation.java
│   │   │           │   └── Invoice.java
│   │   │           ├── repositories
│   │   │           │   ├── UserRepository.java
│   │   │           │   ├── ParkingSlotRepository.java
│   │   │           │   ├── VehicleLogRepository.java
│   │   │           │   ├── ReservationRepository.java
│   │   │           │   └── InvoiceRepository.java
│   │   │           ├── services
│   │   │           │   ├── UserService.java
│   │   │           │   ├── ParkingSlotService.java
│   │   │           │   ├── VehicleLogService.java
│   │   │           │   ├── ReservationService.java
│   │   │           │   └── BillingService.java
│   │   │           └── dtos
│   │   │               ├── UserDTO.java
│   │   │               ├── ParkingSlotDTO.java
│   │   │               ├── VehicleLogDTO.java
│   │   │               ├── ReservationDTO.java
│   │   │               └── InvoiceDTO.java
│   │   └── resources
│   │       ├── application.properties
│   │       └── bootstrap.yml
├── pom.xml
└── README.md
```

## Module Overview

### 1. User Management
- **Features**: Registration, login, and role-based access for admins, staff, and customers.
- **Entities**:
    - `User`: UserID, Name, Email, Phone, Role, Password (hashed).

### 2. Parking Slot Management
- **Features**: Add/remove/update parking slots, check real-time availability.
- **Entities**:
    - `ParkingSlot`: SlotID, Type (2W/4W), IsOccupied, Location.

### 3. Vehicle Entry & Exit Logging
- **Features**: Log entry and exit, calculate duration, and update occupancy.
- **Entities**:
    - `VehicleLog`: LogID, VehicleNumber, EntryTime, ExitTime, SlotID, UserID.

### 4. Reservation System
- **Features**: View availability, reserve slots, modify or cancel reservations.
- **Entities**:
    - `Reservation`: ReservationID, UserID, SlotID, VehicleNumber, StartTime, EndTime, Status.

### 5. Billing and Payments
- **Features**: Dynamic billing based on time and vehicle type, payment processing.
- **Entities**:
    - `Invoice`: InvoiceID, UserID, Amount, PaymentMethod, Status, Timestamp.

## Database Design
| Table Name   | Primary Key   | Foreign Keys         |
|--------------|---------------|----------------------|
| User         | UserID        | –                    |
| ParkingSlot  | SlotID        | –                    |
| VehicleLog   | LogID         | UserID, SlotID       |
| Reservation  | ReservationID | UserID, SlotID       |
| Invoice      | InvoiceID     | UserID               |

## Non-Functional Requirements
- **Performance**: Support 200+ concurrent users in development/test setups.
- **Scalability**: Horizontal scalability using containerization (optional in the future).
- **Security**: Role-based access, encrypted password storage, HTTPS for all data exchange.
- **Usability**: Responsive and mobile-friendly UI, WCAG-compliant design.

## Assumptions and Constraints
- **Assumptions**:
    - Each slot accommodates only one vehicle.
    - Entry/exit operations are manual.
- **Constraints**:
    - SMS/Email notifications are out of scope.
    - Third-party integrations are not included in this phase.
