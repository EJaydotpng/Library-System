# LibrarySys Documentation

## Overview

**LibrarySys** is a web-based library management system built with Laravel. It provides features for librarians and members to manage books, users, and transactions efficiently.

---

## Objectives

- To provide an efficient and user-friendly platform for managing library resources.
- To automate book borrowing, returning, and inventory tracking.
- To enable role-based access for librarians and members.
- To generate reports and track user transactions.
- To enhance learning in system integration and architecture using Laravel.

---

## Features / Functionality

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

## Installation Instructions

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

## Code Snippets

### Authentication Controller (Login & Register)
````php
// filepath: [AuthController.php](http://_vscodecontentref_/0)
public function login(Request $request)
{
    $request->validate([
        'email' => 'required|email',
        'password' => 'required',
    ]);

    if (Auth::attempt($request->only('email', 'password'))) {
        $request->session()->regenerate();
        $user = Auth::user();
        if ($user->role_id == 1){
            return redirect()->route('librarian.dashboard');
        } elseif ($user->role_id == 2){
            return redirect()->route('member.dashboard');
        }
    }
    throw ValidationException::withMessages([
        'email' => ['The provided credentials do not match our records.'],
    ]);
}

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


## Contributors

- **Santiago Elija R. Sabulao Jr.**

- Developed for DMMMSU System Integration and Architecture 2 (AY 2025-26).
