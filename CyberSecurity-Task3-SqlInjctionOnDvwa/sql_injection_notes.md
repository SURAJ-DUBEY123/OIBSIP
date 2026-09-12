# SQL Injection Experiment Notes

## Environment

- Application: Damn Vulnerable Web Application (DVWA)
- Server: XAMPP
- Web Server: Apache
- Database: MariaDB/MySQL
- Security Level: Low
- Testing Environment: Localhost
- Target: DVWA SQL Injection module

## Baseline Test

### Input

`1`

### Result

The application returned:

- ID: 1
- First name: admin
- Surname: admin

This was used as the baseline for comparison.

---

## Payload 1

### Payload

`' OR '1'='1`

### Result

The injection returned multiple database records.

The following records were displayed:

1. admin — admin
2. Gordon — Brown
3. Hack — Me
4. Pablo — Picasso
5. Bob — Smith

### Analysis

The payload introduces an OR condition containing a comparison
that evaluates to true.

Because the application is intentionally vulnerable at Low
security, the user input is incorporated into the SQL query
without proper parameterisation. This changes the logic of the
query and causes multiple records to be returned.

### Evidence

Screenshot: `screenshots/02-payload-1.png`

---

## Payload 2

### Payload

`' OR 1=1 #`

### Result

The injection also returned multiple database records:

1. admin — admin
2. Gordon — Brown
3. Hack — Me
4. Pablo — Picasso
5. Bob — Smith

### Analysis

`1=1` is an expression that always evaluates to true.

The `#` character is interpreted by MySQL/MariaDB as the beginning
of a comment, causing the remainder of the original SQL statement
to be ignored.

Because the application is vulnerable, the modified query returns
multiple records instead of only the intended record.

### Evidence

Screenshot: `screenshots/03-payload-2.png`

---

## Data Exposed

The SQL Injection caused the application to display five database
records instead of only the expected record for User ID 1.

The exposed information included the first names and surnames
stored in the DVWA users table.

---

## Security Impact

SQL Injection can allow unauthorized users to manipulate database
queries and retrieve information that they should not have access
to.

Depending on the vulnerability and database permissions, SQL
Injection can potentially have more serious consequences such as
modifying or deleting data.

---

## Prevention

The primary defense against SQL Injection is the use of
parameterized queries or prepared statements.

Instead of directly concatenating user input into an SQL query,
the application should send the SQL statement and the user data
separately.

Input validation and least-privilege database permissions should
also be used as additional security measures.

---

## Conclusion

The experiment demonstrated a classic SQL Injection vulnerability
in DVWA running locally with the security level set to Low.

Both tested payloads caused multiple records to be returned,
demonstrating that unsanitized user input can alter the logic of
an SQL query.