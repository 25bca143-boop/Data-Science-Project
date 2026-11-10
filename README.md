# Library Management System

## Project overview

This is a small MySQL database project for recording library members, books and book-loan activity. It can be used to practise table creation, relationships, inserting records and retrieving information with SQL.

## Requirements

- MySQL Server
- MySQL Workbench (or another MySQL client)

## Database structure

The database is named `librarydb` and contains three tables:

| Table | Purpose |
|---|---|
| `members` | Stores member names, member type and joining date. |
| `books` | Stores book titles, authors, categories, prices and available-copy counts. |
| `issues` | Records which member borrowed which book, along with issue, due and return dates. |

### Relationships

- One member can have many issue records.
- One book can appear in many issue records.
- `issues.member_id` references `members.member_id`.
- `issues.book_id` references `books.book_id`.

The `issues` table therefore connects members and books through foreign keys.

## Files

| File | Description |
|---|---|
| `library_management.sql` | Creates the database and its three tables. |
| `sample_data.sql` | Inserts the example members, books and borrowing records. |
| `ERD.png` | Shows the entity relationship diagram. |

## How to run

1. Open MySQL Workbench and connect to your MySQL server.
2. Open `library_management.sql` and execute the complete script.
3. Open `sample_data.sql` and execute it after the database and tables have been created.
4. Refresh the Schemas panel and select `librarydb`.
5. Run the checks below to confirm that the records were inserted.

```sql
USE librarydb;

SELECT COUNT(*) AS total_members FROM members;
SELECT COUNT(*) AS total_books FROM books;
SELECT COUNT(*) AS total_issues FROM issues;
```

The supplied sample data contains 12 members, 15 books and 32 issue records.

## Example queries

```sql
-- list all books
SELECT * FROM books;

-- show borrowed books with member names
SELECT
    m.member_name,
    b.title,
    i.issue_date,
    i.due_date,
    i.return_date
FROM issues AS i
JOIN members AS m ON i.member_id = m.member_id
JOIN books AS b ON i.book_id = b.book_id;

-- find books that have no available copies
SELECT title, author
FROM books
WHERE copies_available = 0;

-- find books that have not yet been returned
SELECT
    m.member_name,
    b.title,
    i.due_date
FROM issues AS i
JOIN members AS m ON i.member_id = m.member_id
JOIN books AS b ON i.book_id = b.book_id
WHERE i.return_date IS NULL;
```

## Notes

- A `NULL` value in `return_date` means the book has not yet been marked as returned.
- The sample issue dates use a 14-day borrowing period for students and a 30-day period for faculty.
- The `copies_available` values are sample starting values; they are not automatically changed by the schema script.
- Fine calculation and other library rules can be added as further SQL queries or database logic.

## Conclusion

This project provides a basic relational database for a library. It demonstrates how primary keys, foreign keys and SQL queries can be used to organise and retrieve borrowing information.
"# Data-Science-Project" 
