# Day 15: Simple Login System (JSON File)

## What We'll Build

A simple login system using PHP sessions with users stored in a JSON file.

## Prerequisites

Review these lessons before starting:

- [11-file-handling](../11-file-handling/) - `file_get_contents()`, JSON
- [13-sessions-cookies](../13-sessions-cookies/) - Sessions basics
- [08-forms](../08-forms/) - Form handling with `$_POST`

## Project Structure

```
15-login-system/
├── users.json          # Create this file
├── login.php           # Login form and logic
├── index.php           # Home page (shows login status)
└── logout.php          # Destroy session
```

---

## Step 1: Create `users.json`

Create a JSON file with username as key and password as value.

Add 3 users: admin, kiran, student

**Hint:** See `users.sample.json` for format reference.

---

## Step 2: Create `login.php`

This file handles the login form and authentication.

### PHP Logic (before HTML):

1. Start the session
2. Read `users.json` using `file_get_contents()`
3. Convert JSON to array using `json_decode($json, true)`
4. Initialize `$error = ''`
5. Check if form is submitted using `$_SERVER['REQUEST_METHOD'] === 'POST'`
6. Get username and password from `$_POST`
7. Check if user exists and password matches
8. If valid: store username in `$_SESSION['user']` and redirect to `index.php`
9. If invalid: set error message

### HTML:

1. Show error message if `$error` is not empty
2. Create a form with `method="POST"`
3. Add username input (type="text")
4. Add password input (type="password")
5. Add submit button
6. Add link back to home

---

## Step 3: Create `index.php`

The home page that shows different content based on login status.

### PHP Logic:

1. Start the session
2. Check if user is logged in: `isset($_SESSION['user'])`

### HTML:

1. If logged in: show welcome message with username and logout link
2. If not logged in: show message and login link

---

## Step 4: Create `logout.php`

Simple file to destroy the session (no HTML needed).

1. Start the session
2. Clear session data: `$_SESSION = []`
3. Destroy session: `session_destroy()`
4. Redirect to `index.php`

---

## Running the Project

```bash
cd 15-login-system
php -S localhost:8015
```

Open browser: http://localhost:8015

## Test Credentials

| Username | Password   |
| -------- | ---------- |
| admin    | admin123   |
| kiran    | kiran123   |
| student  | student123 |

## Key Functions Reference

| Function                   | Purpose                  |
| -------------------------- | ------------------------ |
| `session_start()`          | Start/resume session     |
| `file_get_contents()`      | Read file as string      |
| `json_decode($json, true)` | Convert JSON to array    |
| `$_SESSION['key']`         | Store/read session data  |
| `header('Location: url')`  | Redirect to another page |
| `session_destroy()`        | End the session          |

## Important Rules

1. `session_start()` must be called before ANY HTML
2. `header()` must be called before any output
3. Always use `exit` after redirect
