# PostgreSQL Literal Database Simulation

## Description
**PostgreSQL Literal Database Simulation** is a project that leverages advanced PostgreSQL features to simulate a literal database. It optimizes performance by enforcing database operations through custom scripts, ensuring efficient handling of data arrays. This approach enables users to perform standard PostgreSQL commands while maintaining high performance through literal-like database usage.

## Table of Contents

- [Description](#description)
- [How to Use](#how-to-use)
- [Features](#features)
- [Dependencies](#dependencies)
- [Execution](#execution)

## How to Use

### 1. Set Up PostgreSQL
Ensure you have PostgreSQL installed and running on your system. You can download it from the [official PostgreSQL website](https://www.postgresql.org/).

### 2. Initialize the Database
1. Create a new PostgreSQL database.
2. Execute the provided SQL scripts to set up the necessary views, functions, and triggers:
   ```sql
   CREATE VIEW tabela_array_alvo AS 
   (SELECT unnest(tb.id) AS id, unnest(tb.valor) AS valor FROM 
    (SELECT 
       (SELECT valor AS id FROM tabela_array WHERE id=1),
       (SELECT valor AS valor FROM tabela_array WHERE id=2)) AS tb);
   
   CREATE OR REPLACE FUNCTION update_array() RETURNS TRIGGER AS 
   ...
   ```
   Copy the rest of the provided SQL script into your PostgreSQL client.

### 3. Perform Operations
Users can interact with the database using standard SQL commands. The scripts enforce array-based operations through:

- **Insertions**: Automatically update associated arrays.
- **Updates**: Modify array elements efficiently.
- **Deletions**: Ensure consistency by removing array elements.

## Features

- **Array-Based Operations**: Handles data arrays as core components for optimization.
- **Custom Functions**: Leverages PL/pgSQL for specialized operations like `insert_array`, `update_array`, and `delete_array`.
- **Triggers**: Ensures automatic enforcement of data integrity during insert, update, and delete operations.
- **Views for Simplification**: Exposes complex data manipulations as simplified views for easy querying.

## Dependencies

- **PostgreSQL**: Version 11 or higher is recommended.

## Execution

### 1. Using a PostgreSQL Client

1. Open your preferred PostgreSQL client (e.g., psql, pgAdmin).
2. Run the SQL scripts to set up the database structure.
3. Interact with the database using standard SQL queries.

### 2. Example Queries

- **Insert Data**:
  ```sql
  INSERT INTO tabela_array (id, valor) VALUES (1, ARRAY[101, 102, 103]);
  INSERT INTO tabela_array (id, valor) VALUES (2, ARRAY[201, 202, 203]);
  ```

- **Update Data**:
  ```sql
  UPDATE tabela_array_alvo SET valor = 500 WHERE id = 101;
  ```

- **Delete Data**:
  ```sql
  DELETE FROM tabela_array_alvo WHERE id = 101;
  ```
