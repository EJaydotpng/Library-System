# LibrarySys Documentation

## Overview

**LibrarySys** 
> #### This is a Line!
>
> - Another Line.
> - Line Again.
>
>  *This* is the last **Line**.

---

## Features

### Authentication & Roles
- **Login/Register:** Members can register and login. Librarians are added by administrators.
- **Roles:** Supports `librarian` and `member` roles.

### Librarian Dashboard
- **User Management:** Add, edit, or delete members and librarians.
- **Book Management:** Add, edit, or delete books. Track inventory and availability.
- **Transactions:** Record book borrow/return transactions.
- **Reports:** View all transactions and generate usage reports.

### Member Dashboard
- **Available Books:** View all books available for borrowing.
- **Transactions:** View current borrowings and transaction history.

---

## Installation

1. **Clone the repository:**
   ```sh
   git clone <repo-url>
   cd LibrarySys
   ```

2. **Install dependencies:**
   ```sh
   composer install
   npm install
   ```

3. **Environment setup:**
   - Copy `.env.example` to `.env` and configure database credentials.
   - Generate application key:
     ```sh
     php artisan key:generate
     ```

4. **Database setup:**
   - Create your database and update `.env`.
   - Run migrations and seeders:
     ```sh
     php artisan migrate --seed
     ```

5. **Run the application:**
   ```sh
   php artisan serve
   npm run dev
   ```

---

## Usage

### Librarian
- Access dashboard at `/librarian/dashboard`.
- Manage users and books via sidebar links.
- Record transactions and view reports.

### Member
- Access dashboard at `/member/dashboard`.
- View available books and transaction history.

---

## Folder Structure

- `app/Models`: Eloquent models (`User`, `Book`, `Transaction`, `Role`, `Fine`)
- `app/Http/Controllers`: Controllers for authentication, user, book, and transaction management
- `resources/views`: Blade templates for UI
- `routes/web.php`: Route definitions
- `database/migrations`: Database schema
- `database/seeders`: Initial data (roles, etc.)

---

## Database Schema

- **roles**: `role_id`, `name`
- **users**: `user_id`, `username`, `fname`, `mi`, `lname`, `email`, `password`, `role_id`
- **books**: `book_id`, `title`, `author`, `isbn`, `category`, `quantity_total`, `quantity_available`
- **transactions**: `transaction_id`, `user_id`, `book_id`, `borrow_date`, `due_date`, `return_date`, `status`, `quantity`
- **fines**: `fine_id`, `transaction_id`, `amount`, `paid`, `date_paid`

---

## Development

- **Testing:** Run unit and feature tests with:
  ```sh
  php artisan test
  ```
- **Styling:** Uses Tailwind CSS (see `vite.config.js`).

---


## Authors

- Developed for DMMMSU System Integration and Architecture 2 (AY 2025-26).
