# Java Servlet Student Portal

A full-stack web application built with **Java Servlets** and **MySQL**, featuring role-based access control, user authentication, and complete CRUD operations on student records.

---

## Features

- **Authentication** — Login, logout, and new user registration with error handling
- **Role-Based Access** — Separate dashboards and permissions for admins and regular users
- **Student Management** — Create, read, update, and delete student records from a MySQL database

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Java Servlets |
| Server | GlassFish 4.1.1 |
| Database | MySQL 8+ |
| IDE | NetBeans 8.2 |
| JDK | Java 8 |
| DB Driver | MySQL Connector 9.0.0 |

---

## Prerequisites

Make sure the following are installed before running this project:

- [NetBeans 8.2](https://netbeans.apache.org/)
- [JDK 8](https://www.oracle.com/java/technologies/java8.html)
- [GlassFish 4.1.1 Server](https://javaee.github.io/glassfish/)
- [MySQL 8 or higher](https://dev.mysql.com/downloads/)
- [MySQL Connector/J 9.0.0](https://dev.mysql.com/downloads/connector/j/) (`.jar`)

---

## Installation & Setup

### Step 1 — Clone the Repository

```bash
git clone https://github.com/ARYAN0529/CRUD-Example.git
cd CRUD-Example
```

### Step 2 — Configure the Database

Create a MySQL database:

```sql
CREATE DATABASE servlet_crud_example;
USE servlet_crud_example;
```

Run the following SQL to set up the required tables:

```sql
CREATE TABLE user (
  userID   INT          NOT NULL AUTO_INCREMENT,
  username VARCHAR(255) NOT NULL,
  password VARCHAR(255) NOT NULL,
  isAdmin  CHAR(1)      DEFAULT 'F',
  PRIMARY KEY (userID),
  UNIQUE KEY username (username),
  CONSTRAINT true_or_false CHECK (isAdmin = 'T' OR isAdmin = 'F')
);

INSERT INTO user (username, password, isAdmin)
VALUES ('admin', 'admin', 'T');

CREATE TABLE student (
  userid   INT,
  rollno   VARCHAR(255),
  name     CHAR(255),
  gender   CHAR(255),
  age      INT,
  email    VARCHAR(255),
  mobile   VARCHAR(255),
  degree   VARCHAR(255),
  batch    VARCHAR(255),
  section  CHAR(2),
  gpa      FLOAT,
  FOREIGN KEY (userid) REFERENCES user(userID)
);
```

### Step 3 — Update Database Credentials

Open the following files and set your MySQL **username**, **password**, and **database name**:

- `src/dao/UserDao.java`
- `src/dao/StudentDao.java`

### Step 4 — Run the Application

1. Open the project in **NetBeans 8.2**
2. Add the **MySQL Connector JAR** to the project libraries
3. Configure the **GlassFish 4.1.1** server in NetBeans
4. Click **Run Project**
5. Access the app at:

```
http://localhost:8080/ServletCRUDExample
```

---

## Default Admin Credentials

| Field | Value |
|-------|-------|
| Username | `admin` |
| Password | `admin` |

> ⚠️ Change the default admin password after first login.

---

## Project Structure

```
CRUD-Example/
├── src/
│   ├── dao/          # Database access layer (UserDao, StudentDao)
│   ├── model/        # Java model classes
│   └── servlet/      # Servlet controllers
├── web/
│   ├── WEB-INF/
│   └── *.jsp         # JSP view pages
└── README.md
```

---

## License

This project is open source and available under the [MIT License](LICENSE).
