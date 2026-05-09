# Project Report: Airline Ticket Booking System
**Course:** Database Management Systems (DBMS)  
**Date:** April 30, 2026  

---

## 1. Project Overview
This project involves the design and implementation of an **Airline Ticket Booking System**. The system manages core airline operations, including passenger registration, flight scheduling, booking transactions, and payment tracking.

### Team Members:
*   **Neeraj kumar**
*   **Nikhil chandra chaudhary**
*   **Nikhil Kumar**

---

## 2. Entity Relationship (ER) Diagram
Our system design is based on the following ER model. It defines the entities and how they interact within the database environment.

![ER Diagram](er_diagram.jpeg)

**Key Relationships:**
*   **Passenger-Booking (1:M):** A single passenger can make multiple bookings.
*   **Flight-Booking (1:M):** A single flight can accommodate many passengers through multiple bookings.
*   **Booking-Payment (1:1):** Every booking is linked to exactly one payment record to ensure financial integrity.

---

## 3. Database Schema
The database is comprised of four tables. We implemented a **Junction Table** (`booking`) to resolve the many-to-many relationship between passengers and flights.

### Table: Passenger
| Field | Type | Key | Note |
| :--- | :--- | :--- | :--- |
| passenger_id | INT | PRI | Auto-increment identifier. |
| name | VARCHAR | | Full name of the traveler. |
| age | INT | | |
| gender | VARCHAR | | |
| email | VARCHAR | UNI | Added to ensure entity integrity. |

### Table: Flight
| Field | Type | Key | Note |
| :--- | :--- | :--- | :--- |
| flight_id | INT | PRI | Unique flight code. |
| flight_name | VARCHAR | | e.g., IndiGo 6E101. |
| source | VARCHAR | | Departure city. |
| destination| VARCHAR | | Arrival city. |
| price | DECIMAL | | Ticket cost. |

---

## 4. Normalization & Integrity
The database satisfies the requirements for **Third Normal Form (3NF)**:
*   **1NF:** All attributes contain atomic values.
*   **2NF:** No partial dependencies; all non-key attributes depend on the full Primary Key.
*   **3NF:** No transitive dependencies. For example, the `price` depends only on the `flight_id`.

**Constraint Implementation:**
To handle logical redundancy (e.g., multiple passengers with the same name), we enforced a `UNIQUE` and `NOT NULL` constraint on the `email` column.

---

## 5. Essential SQL Queries

### A. The "Triple Join" (Passenger Manifest)
This query retrieves a complete list of passengers, the flights they are on, and the dates they are traveling.
```sql
SELECT 
    p.name AS 'Passenger Name', 
    f.flight_name AS 'Flight', 
    f.source, 
    f.destination, 
    b.booking_date
FROM booking b
JOIN passenger p ON b.passenger_id = p.passenger_id
JOIN flight f ON b.flight_id = f.flight_id;# Airline_TicketBooking_2CSE24_G9
