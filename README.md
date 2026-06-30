# 🛒 PHP E-Commerce Platform

A full-stack e-commerce web application built with **PHP, MySQL (PDO), HTML, CSS**, featuring separate **Customer** and **Admin** experiences — secure authentication, product management, and a shopping cart system.

![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)

![Home Page Preview](http://localhost/ECOMMERCE/index.php)

---

## 📖 Overview

This project is a lightweight, from-scratch e-commerce platform built using **vanilla PHP and MySQL** (no frameworks), demonstrating core full-stack development skills: relational database design, secure session-based authentication, CRUD operations, and clean separation between customer-facing and admin-facing modules.

It was built to practice and showcase:
- Secure user authentication & password hashing
- Role-based access control (Customer vs Admin)
- CRUD operations on a relational database
- Session management
- Clean, responsive UI with custom CSS

---

## ✨ Features

### 👤 Customer
- User registration with hashed passwords
- Secure login / logout with session handling
- Browse all available products on the homepage
- Add products to a personal shopping cart
- View, update quantity, or remove items from the cart with live total calculation

### 🛠️ Admin
- Dedicated, role-protected admin login
- Centralized admin dashboard
- Add new products (with image upload)
- View, edit, and delete products in a management table

### 🔒 Security
- Passwords hashed using PHP's `password_hash()` / verified with `password_verify()`
- Prepared statements (PDO) throughout to prevent SQL injection
- Session-based access control for both customer and admin protected routes
- Role-based authorization via a `role` column (`user` / `admin`)

---

## 🧰 Tech Stack

| Layer          | Technology               |
|----------------|---------------------------|
| Backend        | PHP (procedural, PDO)     |
| Database       | MySQL                     |
| Frontend       | HTML5, CSS3               |
| Auth & Sessions| PHP Sessions, `password_hash()` |

---

## 🗂️ Project Structure

```
ecommerce/
├── admin/
│   ├── login.php           # Admin login
│   ├── logout.php          # Admin logout
│   ├── dashboard.php       # Admin control panel
│   ├── add_product.php     # Add new product (with image upload)
│   └── manage_products.php # View / edit / delete products
├── pages/
│   ├── register.php        # User registration
│   ├── login.php           # User login
│   ├── logout.php          # User logout
│   └── cart.php            # Shopping cart management
├── includes/
│   └── db.php              # PDO database connection
├── images/                 # Uploaded product images
├── css/
│   └── style.css           # Site-wide styling
└── index.php                # Homepage – product listing
```

---

## 🗄️ Database Schema

**`users`** — stores customer and admin accounts

| Column     | Type                          |
|------------|--------------------------------|
| id         | INT, AUTO_INCREMENT, PK       |
| username   | VARCHAR(50)                   |
| email      | VARCHAR(100), UNIQUE          |
| password   | VARCHAR(255) (hashed)         |
| role       | ENUM('user','admin')          |
| created_at | TIMESTAMP                     |

**`products`** — stores product catalog

| Column      | Type           |
|-------------|----------------|
| id          | INT, AUTO_INCREMENT, PK |
| name        | VARCHAR(255)   |
| price       | DECIMAL(10,2)  |
| description | TEXT           |
| image       | VARCHAR(255)   |
| created_at  | TIMESTAMP      |

**`cart`** — links users to products with quantities

| Column     | Type        |
|------------|-------------|
| id         | INT, AUTO_INCREMENT, PK |
| user_id    | INT (FK → users.id) |
| product_id | INT (FK → products.id) |
| quantity   | INT         |
| created_at / updated_at | TIMESTAMP |

---

## 🚀 Getting Started

### Prerequisites
- PHP 7.4+ (with PDO MySQL extension)
- MySQL / MariaDB
- A local server stack (XAMPP, WAMP, MAMP, or Laragon)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>
   ```

2. **Set up the database**
   - Create a database named `ecommerce` in phpMyAdmin or via MySQL CLI.
   - Run the SQL scripts (see `Database Schema` above or `/database/schema.sql` if included) to create the `users`, `products`, and `cart` tables.

3. **Configure the database connection**
   - Open `includes/db.php` and update credentials if needed:
     ```php
     $host = 'localhost';
     $dbname = 'ecommerce';
     $user = 'root';
     $password = '';
     ```

4. **Create an admin account**
   Since there is no public admin registration page (by design, for security), insert an admin directly:
   ```sql
   INSERT INTO users (username, email, password, role, created_at)
   VALUES ('Admin Name', 'admin@example.com', '<hashed_password>', 'admin', NOW());
   ```
   > Generate the hashed password using PHP's `password_hash('yourpassword', PASSWORD_DEFAULT)`.

5. **Run the project**
   - Place the project folder inside your server's root (e.g., `htdocs` for XAMPP).
   - Start Apache & MySQL.
   - Visit `http://localhost/ecommerce/index.php` in your browser.

---

## 🔐 Why Is There No Admin Registration Page?

This is an intentional security decision, not an oversight:
- Open admin registration would create a serious attack surface.
- Admin accounts are provisioned manually by trusted personnel via direct database access.
- A single `users` table with a `role` field keeps the schema simple while still enforcing access control at the application layer.

---

## 🗺️ Roadmap / Future Improvements

- [ ] Add order checkout & payment gateway integration
- [ ] Add order history for customers
- [ ] Add product categories and search/filter
- [ ] Migrate to a PHP framework (Laravel) for scalability
- [ ] Add input validation & CSRF protection
- [ ] Write automated tests (PHPUnit)

---

## 📸 Screenshots

| Home Page | Register |
|:---:|:---:|
| ![Home Page](http://localhost/ECOMMERCE/index.php) | ![Register Page](./screenshots/register.png) |

| Login | Cart |
|:---:|:---:|
| ![Login Page](./screenshots/login.png) | ![Cart Page](./screenshots/cart.png) |

| Cart — Quantity Update |
|:---:|
| ![Cart Update](./screenshots/cart_update.png) |

---

## 👨‍💻 Author

**Chaitanya Pappala**
[GitHub] (https://github.com/chaitanyapappalatech) · [LinkedIn] (https://www.linkedin.com/in/chaitanya-sd/)· [Portfolio](http://localhost/ECOMMERCE/index.php)

---

