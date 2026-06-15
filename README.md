# ⚽ Football Ticket Booking Database Design & SQL Queries

A simple PostgreSQL database project for managing football matches, users, and ticket bookings. This project demonstrates database design concepts such as table relationships, constraints, data seeding, and SQL queries.

---

# 📋 Project Overview

The system manages:

* **Users** (Football Fans and Ticket Managers)
* **Football Matches**
* **Ticket Bookings**

The project also includes several SQL queries demonstrating:

* Filtering data
* Searching records
* Handling `NULL` values
* `JOIN` operations
* Subqueries
* Pagination using `LIMIT` and `OFFSET`

---

# 🗄️ Database Schema

## 1. Users Table

Stores information about users of the system.

| Column       | Data Type    | Constraints                              |
| ------------ | ------------ | ---------------------------------------- |
| user_id      | SERIAL       | Primary Key                              |
| full_name    | VARCHAR(100) | NOT NULL                                 |
| email        | VARCHAR(100) | UNIQUE, NOT NULL                         |
| role         | VARCHAR(20)  | CHECK ('Ticket Manager', 'Football Fan') |
| phone_number | VARCHAR(20)  | Nullable                                 |

---

## 2. Matches Table

Stores football match information.

| Column              | Data Type     | Constraints  |
| ------------------- | ------------- | ------------ |
| match_id            | SERIAL        | Primary Key  |
| fixture             | VARCHAR(150)  | NOT NULL     |
| tournament_category | VARCHAR(100)  | NOT NULL     |
| base_ticket_price   | DECIMAL(10,2) | CHECK >= 0   |
| match_status        | VARCHAR(20)   | CHECK values |

### Allowed Match Statuses

* Available
* Selling Fast
* Sold Out
* Postponed

---

## 3. Bookings Table

Stores ticket booking information.

| Column         | Data Type     | Constraints |
| -------------- | ------------- | ----------- |
| booking_id     | SERIAL        | Primary Key |
| user_id        | INT           | Foreign Key |
| match_id       | INT           | Foreign Key |
| seat_number    | VARCHAR(20)   | Nullable    |
| payment_status | VARCHAR(20)   | Nullable    |
| total_cost     | DECIMAL(10,2) | CHECK >= 0  |

### Allowed Payment Statuses

* Pending
* Confirmed
* Cancelled
* Refunded

---

# 🔗 Database Relationships

## Users → Bookings

* One user can have multiple bookings.
* One booking belongs to one user.

Relationship:

```text
Users (1) --------< Bookings (M)
```

---

## Matches → Bookings

* One match can have multiple bookings.
* One booking belongs to one match.

Relationship:

```text
Matches (1) --------< Bookings (M)
```

---

## Users ↔ Matches

Users and Matches have a **Many-to-Many** relationship through the `Bookings` table.

```text
Users (M) --------< Bookings >-------- (M) Matches
```

---

# 📊 ER Diagram

```text
        USERS
    +---------------+
    | PK user_id    |
    | full_name     |
    | email         |
    | role          |
    | phone_number  |
    +---------------+
            |
            | 1
            |
            | M
      +----------------+
      |    BOOKINGS    |
      +----------------+
      | PK booking_id  |
      | FK user_id     |
      | FK match_id    |
      | seat_number    |
      | payment_status |
      | total_cost     |
      +----------------+
            |
            | M
            |
            | 1
            |
      +---------------+
      |    MATCHES    |
      +---------------+
      | PK match_id   |
      | fixture       |
      | tournament... |
      | base_ticket...|
      | match_status  |
      +---------------+
```

---

# 🌱 Sample Data

The database contains:

* 4 Users
* 5 Matches
* 5 Bookings

---

# 📝 SQL Queries Included

## Query 1

Retrieve all available Champions League matches.

---

## Query 2

Search users whose:

* Name starts with `Tanvir`
* Name contains `Haque`

---

## Query 3

Retrieve bookings with missing payment status and replace `NULL` using `COALESCE`.

---

## Query 4

Retrieve booking details along with user name and match fixture using `INNER JOIN`.

---

## Query 5

Display all users and their bookings using `LEFT JOIN`.

---

## Query 6

Find bookings whose total cost is greater than the average booking cost using a subquery.

---

## Query 7

Retrieve the top two expensive matches while skipping the highest-priced match using `OFFSET` and `LIMIT`.

---

# 🚀 Technologies Used

* PostgreSQL
* Beekeeper Studio

---

# 📂 Project Structure

```text
Level2-B7A3/
│
├── requerements
├── QUERY.sql
├── solution.sql
└── README.md
```

---

# 🎯 Learning Objectives

This project demonstrates:

* Database Design
* Primary Keys
* Foreign Keys
* One-to-Many Relationships
* Many-to-Many Relationships
* Constraints
* Joins
* Subqueries
* Aggregate Functions
* NULL Handling
* Pagination Queries

---

# 👨‍💻 Author

Developed as a practice project for learning PostgreSQL database design and SQL querying.
