# SQL Injection on DVWA

## OASIS INFOBYTE — Cyber Security Task 3

## Objective

The objective of this task was to demonstrate a classic SQL
Injection vulnerability using Damn Vulnerable Web Application
(DVWA) running on a local XAMPP server.

The experiment was performed only on the local DVWA environment.

---

## Technologies and Tools Used

- DVWA (Damn Vulnerable Web Application)
- XAMPP
- Apache Web Server
- PHP
- MariaDB/MySQL
- Web Browser
- Windows

---

## What is DVWA?

DVWA stands for Damn Vulnerable Web Application.

It is a deliberately vulnerable web application designed for
security training and learning. It contains several intentionally
vulnerable modules, including SQL Injection.

For this task, the SQL Injection module was used.

---

## Environment Setup

The application was installed and configured on a local Windows
machine using XAMPP.

XAMPP provided:

- Apache for serving the DVWA web application
- MariaDB/MySQL for the database
- PHP for executing the DVWA application
- phpMyAdmin for database management

The application was accessed through localhost.

Example:

`http://localhost/dvwa/`

---

## DVWA Security Level

The DVWA security level was set to:

**Low**

The Low security setting was used because the objective was to
demonstrate the SQL Injection vulnerability in a controlled
environment.

Evidence:

`screenshots/00-security-low.png`

---

## SQL Injection

SQL Injection is a web application vulnerability that occurs when
untrusted user input is incorporated into an SQL query without
properly separating the input from the SQL code.

An attacker can manipulate the input so that the database
interprets part of the input as SQL syntax.

---

## Baseline Test

The initial input was:

`1`

The application returned:

- ID: 1
- First name: admin
- Surname: admin

This established the normal behavior of the application.

Evidence:

`screenshots/01-normal-query.png`

---

## SQL Injection Payload 1

### Payload

`' OR '1'='1`

### Result

The payload caused multiple database records to be returned.

The following records were displayed:

- admin — admin
- Gordon — Brown
- Hack — Me
- Pablo — Picasso
- Bob — Smith

Instead of returning only the record associated with User ID 1,
the application returned five records.

Evidence:

`screenshots/02-payload-1.png`

---

## Why Payload 1 Works

The payload introduces an OR condition containing:

`'1'='1'`

This condition is always true.

Because the application is vulnerable and does not properly
separate user input from SQL syntax, the injected condition changes
the logic of the SQL query.

As a result, multiple records can satisfy the query.

---

## SQL Injection Payload 2

### Payload

`' OR 1=1 #`

### Result

The second payload also returned five records:

- admin — admin
- Gordon — Brown
- Hack — Me
- Pablo — Picasso
- Bob — Smith

Evidence:

`screenshots/03-payload-2.png`

---

## Why Payload 2 Works

The expression:

`1=1`

is always true.

The `#` character is treated as a comment marker by MySQL/MariaDB.
This can cause the remaining part of the original SQL statement to
be ignored.

The vulnerable application therefore processes the modified query
and returns multiple records.

---

## Data Exposed

The injection exposed information from multiple records in the
DVWA database.

The displayed information included:

- The value processed as the User ID input
- First names
- Surnames

Five records were returned during each successful injection test.

---

## Security Impact

SQL Injection can allow an attacker to access database information
that they were not authorized to view.

In more serious situations, SQL Injection may also allow data to be
modified or deleted, depending on the application's database
permissions and the specific vulnerability.

---

## How to Prevent SQL Injection

The primary defense is to use parameterized queries or prepared
statements.

### Vulnerable approach

A vulnerable application may construct an SQL query by directly
concatenating user input into the query.


### Vulnerable approach

A vulnerable application may construct an SQL query by directly
concatenating user input into the query.

Conceptually:

```php
$query = "SELECT * FROM users WHERE id = '$input'";

Conceptually:

```php
$query = "SELECT * FROM users WHERE id = '$input'";

This allows the input to influence the SQL syntax.

Safer approach

A prepared statement separates the SQL command from the user data.

Example:
$stmt = $pdo->prepare(
    "SELECT * FROM users WHERE id = :id"
);

$stmt->execute([
    ':id' => $input
]);

The database then treats the supplied value as data rather than
as part of the SQL command.

Additional security measures include:

Input validation
Least-privilege database accounts
Proper error handling
Avoiding unnecessary database permissions

Ethical Considerations

This experiment was performed only against DVWA running locally on
the user's own machine.

No real website, external server, or third-party service was
targeted.

DVWA is specifically designed to provide a controlled environment
for practicing web application security.

Conclusion

The experiment successfully demonstrated a classic SQL Injection
vulnerability in DVWA at Low security.

Two different SQL Injection payloads were tested and both caused
multiple database records to be returned.

The experiment demonstrates why applications should never directly
incorporate untrusted user input into SQL queries.

Parameterized queries and prepared statements provide the primary
defense against this vulnerability.