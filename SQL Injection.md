 # SQL Injection

**SQL Injection** is a security vulnerability in which an attacker can manipulate a web application’s database query by inserting malicious SQL statements into input fields, URLs, or headers. This can allow unauthorized access to data, modification of database content, or even full control over the backend database system. SQL injection occurs when applications do not properly sanitize user inputs before embedding them in SQL queries, making them vulnerable to crafted injections.

## How SQL Injection Works:

In SQL injection attacks, attackers insert specially crafted SQL code into an input field (like a login form) to change the logic of SQL queries. For example, entering `"' OR '1'='1"` into a username field in an unsecured application could change an authentication query from.

  

Key elements of SQL Injection:

- **User-Controlled Inputs** directly impact the SQL query due to lack of validation.
- **Query Manipulation** enables attackers to bypass authentication, access unauthorized data, delete records, or escalate privileges.
- **Mitigations** include using parameterized queries, prepared statements, or Object-Relational Mapping (ORM) libraries to avoid direct SQL query building. Additionally, validating and sanitizing user inputs can help prevent these attacks.

  

We test the `POST` request to the `/apply_coupon` endpoint in BurpSuit, with JSON data containing the `coupon_code` and `amount` fields.

  
An SQL Injection is attempted by manipulating the `coupon_code` value with a string: `"0' or '0' = '0"`. This is a basic SQL injection attempt, using the `'OR'` operator to test if the endpoint is vulnerable by always making the conditional true (`'0' = '0'`).

The server responds with a message indicating that the coupon has already been claimed, which suggests that the application did not execute the injection, possibly due to input validation or server-side restrictions on the coupon logic.

![](/images/image%2065.png)

  

A more advanced SQL injection is attempted: `"0'; select version() --"`. Here, `select version()` is a SQL command that retrieves the database version, a common SQL Injection payload to determine if the server executes arbitrary SQL. The `-` symbol comments out the rest of the SQL statement, effectively closing the query safely for injection.

The server responds with a success message and returns the PostgreSQL database version in the response, confirming a successful SQL Injection. This confirms that the input field is vulnerable and allows arbitrary SQL commands.

![](/images/image%2066.png)

## To mitigate SQL Injection vulnerabilities in APIs:



### 1. **Parameterized Queries and Prepared Statements**

Parameterized queries and prepared statements separate SQL code from data, ensuring that any data passed as parameters cannot be executed as part of the SQL command.

- Ensure all database queries in the application use parameterized statements where input values are bound as parameters, not directly injected into SQL strings.
- For example, instead of directly inserting `coupon_code` into the query, bind it as a parameter using a placeholder in SQL: `SELECT * FROM coupons WHERE code = ?`, where `?` is replaced securely.

**Industry Standard Tools**: Modern database libraries and frameworks like **JDBC (Java)**, **PDO (PHP)**, and **ORM libraries (like SQLAlchemy for Python)** natively support parameterized queries.

### 2. **ORM (Object-Relational Mapping) Frameworks**

ORM frameworks automatically generate SQL queries based on data models, minimizing direct SQL usage and reducing SQL injection risks. Most ORMs use parameterized queries internally, providing additional security.

- Adopt ORM libraries to abstract away SQL query creation. Use built-in methods for database operations instead of raw SQL queries, as ORM methods handle parameter binding securely.
- Many ORMs allow developers to interact with databases through a high-level API, automatically managing query structure and binding parameters.

**Industry Standard Tools**: **Hibernate (Java)**, **Entity Framework (C#)**, **Django ORM (Python)**, and **Sequelize (Node.js)** are popular ORM frameworks that help secure database interactions by default.

### 3. **Web Application Firewalls (WAFs)**

A Web Application Firewall (WAF) monitors, filters, and blocks malicious HTTP requests, adding an additional layer of protection against SQL injection attacks. WAFs detect and block suspicious patterns in incoming requests that match known SQL injection techniques.

- Deploy a WAF to monitor and protect against SQL injection attacks in real-time. Configure the WAF to block SQL-specific syntax or known SQL injection patterns.
- Many WAFs provide automatic rule updates to stay up-to-date with the latest attack vectors, providing continuous protection.

**Industry Standard Tools**: **AWS WAF**, **Cloudflare WAF**, **Akamai Kona Site Defender**, and **Imperva WAF** are leading WAF solutions that offer real-time protection against SQL injection.

### 4. **Database Access Control and Least Privilege**

Restrict database permissions to enforce the principle of least privilege, ensuring that each database user only has the necessary permissions to perform their tasks. This limits the potential damage of SQL injection if an attack does occur.

- Create distinct database roles with minimal permissions, restricting each application's database account to only the operations it needs (e.g., SELECT, INSERT, UPDATE).
- Avoid using high-privilege accounts (like admin or root) for application access. Instead, set up separate, lower-privilege accounts for each part of the application.

**Industry Standard Tools**: **AWS IAM** (for AWS-managed databases), **Azure SQL Role-Based Access Control (RBAC)**, **PostgreSQL Role Management**, and **MySQL User Management** provide fine-grained access control and support role-based permissions for database security.