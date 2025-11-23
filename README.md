# Apply Filters to SQL Queries - Security Audit Portfolio

## Project Description

As a security professional at a large organization, I investigated potential security issues involving login attempts and employee machines. This portfolio demonstrates my ability to use SQL with filters to:

- Retrieve specific information from databases
- Investigate security incidents
- Filter data using AND, OR, and NOT operators
- Query employee and login attempt records

The organization's database contains two tables:
- **log_in_attempts**: Records of all login attempts
- **employees**: Information about all employees

---

## Database Schema

### log_in_attempts Table
| Column | Description |
|--------|-------------|
| event_id | Identification number for each login event |
| username | Username of the employee |
| login_date | Date of the login attempt |
| login_time | Time of the login attempt |
| country | Country where login occurred |
| ip_address | IP address of the machine |
| success | Success status (0 = failed, FALSE = failed) |

### employees Table  
| Column | Description |
|--------|-------------|
| employee_id | Identification number for each employee |
| device_id | Device assigned to employee |
| username | Username of the employee |
| department | Employee's department |
| office | Employee's office location |

---

## SQL Queries and Analysis

### 1. Retrieve After-Hours Failed Login Attempts

**Scenario**: Investigate a potential security incident that occurred after business hours. Need to query failed login attempts that occurred after 18:00.

**Query**:
```sql
SELECT * 
FROM log_in_attempts 
WHERE login_time > '18:00' AND success = 0;
```

**Explanation**: 
- Filters the `log_in_attempts` table for entries after 18:00
- Uses `AND` operator to also filter for failed attempts (success = 0)
- Returns all failed login attempts that occurred after hours

---

### 2. Retrieve Login Attempts on Specific Dates

**Scenario**: A suspicious event occurred on 2022-05-09. Need to investigate all login attempts on this date and the day before (2022-05-08).

**Query**:
```sql
SELECT * 
FROM log_in_attempts 
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```

**Explanation**:
- Uses `OR` operator to filter for either date
- Returns all login attempts from both 2022-05-09 and 2022-05-08
- Helps identify patterns across the two-day period

---

### 3. Retrieve Login Attempts Outside of Mexico

**Scenario**: Suspicious login activity was determined to not originate from Mexico. Need to investigate all login attempts that occurred outside of Mexico.

**Query**:
```sql
SELECT * 
FROM log_in_attempts 
WHERE country NOT LIKE 'MEX%';
```

**Explanation**:
- Uses `NOT LIKE` with wildcard pattern 'MEX%' to exclude Mexico
- The `%` wildcard matches any country value starting with "MEX" (including "MEX" and "MEXICO")
- Returns all login attempts from countries other than Mexico

---

### 4. Retrieve Employees in Marketing (East Building)

**Scenario**: Security updates needed for specific employee machines in the Marketing department, located in all offices in the East building (East-170, East-320, etc.).

**Query**:
```sql
SELECT * 
FROM employees 
WHERE department = 'Marketing' AND office LIKE 'East%';
```

**Explanation**:
- Filters for Marketing department employees
- Uses `LIKE 'East%'` to match all East building offices
- The `AND` operator ensures both conditions are met
- Returns all Marketing employees in the East building

---

### 5. Retrieve Employees in Finance or Sales

**Scenario**: Different security update needed for machines in the Finance and Sales departments.

**Query**:
```sql
SELECT * 
FROM employees 
WHERE department = 'Finance' OR department = 'Sales';
```

**Explanation**:
- Uses `OR` operator to include employees from either department
- Returns all employees in Finance OR Sales
- Allows targeting of multiple departments with a single query

---

### 6. Retrieve All Employees Not in IT

**Scenario**: One more security update for employees NOT in the Information Technology department (employees in IT already received this update).

**Query**:
```sql
SELECT * 
FROM employees 
WHERE department != 'Information Technology';
```

**Alternative using NOT**:
```sql
SELECT * 
FROM employees 
WHERE NOT department = 'Information Technology';
```

**Explanation**:
- Uses `NOT` operator (or `!=`) to exclude Information Technology department
- Returns all employees in departments other than IT
- Ensures IT employees are not included in this update

---

## Summary

This portfolio demonstrates my proficiency in:

1. **SQL Filtering**: Successfully applied WHERE clauses to filter database records based on specific criteria

2. **Logical Operators**: 
   - Used `AND` to require multiple conditions to be true simultaneously
   - Used `OR` to include records meeting any of several conditions  
   - Used `NOT` to exclude specific records from results

3. **Pattern Matching**: Implemented `LIKE` operator with wildcards (%) to match partial strings, enabling flexible searches for:
   - Office locations (East%)
   - Country codes (MEX%)

4. **Security Investigation**: Applied these SQL skills to:
   - Investigate failed login attempts after business hours
   - Analyze login attempts on specific dates
   - Identify suspicious activity from specific geographic locations
   - Target specific employee groups for security updates

5. **Database Querying**: Worked with multiple tables (log_in_attempts and employees) to extract relevant security information

These SQL filtering techniques are essential for security auditing, incident response, and maintaining organizational security posture.

---

## Skills Demonstrated

- SQL Query Writing
- Database Filtering and Searching  
- Security Incident Investigation
- Logical Operators (AND, OR, NOT)
- Pattern Matching (LIKE, wildcards)
- Data Analysis for Security

---

**Note**: All queries were executed in a MariaDB shell environment as part of a security audit portfolio project.
