# Hospital-database
# Hospital Management Database — MySQL Teaching Project

A practical MySQL teaching project built around a **synthetic hospital management database**.

The project was created as a classroom example to demonstrate relational database design and progressively introduce common SQL techniques—from creating tables and inserting records to joins, filtering, `CASE` expressions, and subqueries.

> **Data notice:** All patient names, IDs, phone numbers, diagnoses, and financial values are synthetic classroom data. No real patient records are used.

## Database Structure

The database contains three related tables:

| Table | Purpose |
|---|---|
| `patient` | Patient demographics, diagnosis, blood group, and payment status |
| `payment` | Bills, payments, balances, and payment packages |
| `discharge` | Discharge contact/relationship information |

### Relationships

```text
                    ┌──────────────┐
                    │   patient    │
                    │ patient_no PK│
                    └──────┬───────┘
                           │
             ┌─────────────┴─────────────┐
             │                           │
             ▼                           ▼
      ┌──────────────┐           ┌──────────────┐
      │   payment    │           │  discharge   │
      │ patient_no FK│           │ patient_no FK│
      └──────────────┘           └──────────────┘
```

## SQL Concepts Demonstrated

- Database creation with `CREATE DATABASE`
- Table creation with `CREATE TABLE`
- Primary keys
- Foreign keys
- `ENUM`
- `INSERT INTO`
- `SELECT`
- Column aliases
- `CONCAT()`
- Arithmetic expressions
- `SUM()`
- `COUNT()`
- `MIN()`
- `MAX()`
- `AVG()`
- `JOIN`
- Multi-table joins
- `ORDER BY`
- `LIMIT`
- `GROUP BY`
- `WHERE`
- `BETWEEN`
- `IN`
- `LIKE`
- `%` wildcards
- `CASE`
- Subqueries
- `ALTER TABLE`
- `UPDATE`
- `DELETE`

## Repository Structure

```text
hospital-sql-teaching-project/
│
├── README.md
├── hospital_teaching_project.sql
│
└── sql/
    ├── 01_database_schema.sql
    ├── 02_sample_data.sql
    ├── 03_basic_queries.sql
    ├── 04_joins_and_aggregations.sql
    ├── 05_filtering_and_case.sql
    ├── 06_subqueries.sql
    └── 07_alter_update_delete.sql
```

## How to Run

### MySQL Workbench

1. Open MySQL Workbench.
2. Open `hospital_teaching_project.sql`.
3. Execute the script from top to bottom.
4. Refresh the Schemas panel and select the `hospital` database.

### For teaching

The numbered files can be executed individually to teach the concepts progressively:

1. **Database Schema** — create the database and tables.
2. **Sample Data** — populate the tables.
3. **Basic Queries** — retrieve and calculate information.
4. **Joins & Aggregations** — combine tables and summarize data.
5. **Filtering & CASE** — apply conditions and classify records.
6. **Subqueries** — query using results from another query.
7. **ALTER / UPDATE / DELETE** — modify structure and data.

## Example: Joining Patient and Payment Data

```sql
SELECT
    p.patient_no,
    CONCAT(p.first_name, ' ', p.last_name) AS full_name,
    p.diagnosis,
    p.gender,
    pay.bill,
    pay.balance
FROM patient AS p
JOIN payment AS pay
    ON p.patient_no = pay.patient_no;
```

## Example: Finding Patients With Outstanding Balances

```sql
SELECT *
FROM patient
WHERE patient_no IN (
    SELECT patient_no
    FROM payment
    WHERE balance > 0
);
```

## Example: Using CASE

```sql
SELECT
    first_name,
    age,
    CASE
        WHEN age > 60 THEN 'Elderly'
        WHEN age >= 50 THEN 'Adult'
        WHEN age >= 35 THEN 'Young Adult'
        WHEN age >= 20 THEN 'Youth'
        ELSE 'Adolescent'
    END AS age_status
FROM patient;
```

## Classroom Learning Progression

```text
Database
   ↓
Tables & Relationships
   ↓
INSERT / SELECT
   ↓
Functions & Calculations
   ↓
JOIN
   ↓
ORDER BY / LIMIT / GROUP BY
   ↓
WHERE / IN / BETWEEN / LIKE
   ↓
CASE
   ↓
Subqueries
   ↓
ALTER / UPDATE / DELETE
```

## Notes on the Original Teaching Script

The original classroom script intentionally contains examples written for teaching rather than production database deployment. For example, it demonstrates different SQL techniques one at a time, sometimes using repeated `SELECT *` statements or deliberately simple expressions.

For a production database, additional constraints, normalization decisions, indexes, audit fields, validation rules, and data-integrity controls would normally be considered.

## Author

**Egorke Ediri Aiyetan**

Data Analyst | SQL & Data Analytics Instructor

- GitHub: https://github.com/Ediritheanalyst
- LinkedIn: https://www.linkedin.com/in/ediri-egorke-01630b1b7

## Disclaimer

This repository is for educational purposes. The dataset is synthetic and should not be treated as real medical, personal, or financial information.
