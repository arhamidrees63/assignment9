# Module 9 - FastAPI with PostgreSQL and pgAdmin (IS601)

## 📌 Objective
This project demonstrates how to set up a FastAPI web application using **Docker Compose** with **PostgreSQL** and **pgAdmin**.  
It also shows basic database operations including creating tables, inserting records, querying, updating, and deleting data.

## 🐳 Docker Hub Image
You can pull the Docker image directly from my Docker Hub repository:  
👉 **[`arhamidrees63/module9`](https://hub.docker.com/r/arhamidrees63/module9)**


---

## 🧰 Project Setup

### 1. Clone the Repository
```bash
git clone git@github.com:arhamidrees63/assignment9.git
cd assignment9
2. Start Docker Services
Run the following command to build and start all containers:

bash
Copy code
docker compose up --build
Once running:

FastAPI: http://localhost:8000

pgAdmin: http://localhost:5050

🧩 Database Configuration
PostgreSQL Credentials
These match what is defined inside docker-compose.yml:

Setting	Value
Host	db
User	postgres
Password	postgres
Database	fastapi_db
Port	5432

🧮 SQL Commands Used
Below are the SQL commands executed inside pgAdmin → Query Tool to demonstrate database functionality.

(A) Create Tables
sql
Copy code
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE calculations (
    id SERIAL PRIMARY KEY,
    operation VARCHAR(20) NOT NULL,
    operand_a FLOAT NOT NULL,
    operand_b FLOAT NOT NULL,
    result FLOAT NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    user_id INTEGER NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
(B) Insert Records
sql
Copy code
INSERT INTO users (username, email)
VALUES 
('alice', 'alice@example.com'),
('bob', 'bob@example.com');

INSERT INTO calculations (operation, operand_a, operand_b, result, user_id)
VALUES
('add', 2, 3, 5, 1),
('divide', 10, 2, 5, 1),
('multiply', 4, 5, 20, 2);
(C) Query Data
sql
Copy code
SELECT * FROM users;
SELECT * FROM calculations;

SELECT u.username, c.operation, c.operand_a, c.operand_b, c.result
FROM calculations c
JOIN users u ON c.user_id = u.id;
(D) Update a Record
sql
Copy code
UPDATE calculations
SET result = 6
WHERE id = 1;
(E) Delete a Record
sql
Copy code
DELETE FROM calculations
WHERE id = 2;