# SQLite

SQLite is a **lightweight, self-contained, serverless** relational database engine. It is widely used for embedded database applications and small to medium-sized projects.

## Key Features

- **Serverless**: No separate server process — the database engine runs in the same process as the application.
- **Zero Configuration**: No setup or administration required.
- **Cross-Platform**: Works on Windows, macOS, Linux, iOS, Android, and more.
- **Single File Database**: The entire database is stored in a single disk file.
- **ACID Compliance**: Supports atomic, consistent, isolated, and durable transactions.
- **Compact**: The library size is small and efficient.
- **Public Domain**: Free for any use, including commercial.

## Common Use Cases

- Mobile apps (iOS, Android)
- Desktop applications
- Small to medium websites
- Testing and prototyping
- IoT devices

## Basic Usage Example

```sql
-- Create a table
CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  email TEXT UNIQUE NOT NULL
);

-- Insert data
INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');

-- Query data
SELECT * FROM users;
