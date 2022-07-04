# Indexing In Action

1. Create Postgrest Table with million Rows
 - Create docker 
    ```
    docker run -e POSTGRES_PASSWORD=postgres --name pg1 postgres
    ```
    ```
    docker exec -it pg1 psql -U postgres
    ```
-   Create Table
    ```
    CREATE TABLE temp(t int);
    ```
-  Insert million rows
    ```
    INSERT INTO temp(t) SELECT random()*100 from generate_series(0,1000000);
    ```
-  Check 
    ```
    SELECT COUNT(*) FROM temp;
    ```
2. Geting Started with Indexing
-  Check table info
    ```
    \d employees
    ```
- Check cost of query
    ```
    EXPLAIN ANALYZE SELECT id from employees where id = 2000;
    ```
    > Index Only Scan
- Check cost of query column name
    ```
    EXPLAIN ANALYZE SELECT name from employees where id = 5000;
    ```
    > Index Scan Using
- Check query where name
    ```
    EXPLAIN ANALYZE SELECT id from employees where name = `Zs`;

    EXPLAIN ANALYZE SELECT id from employees where name like `Zs`;
    ```
- Create Index
    ```
    CREATE INDEX employees_name on employees(name);
    ```
- Check Again
    ```
    EXPLAIN ANALYZE SELECT id from employees where name like`Zs`;

    EXPLAIN ANALYZE SELECT id from employees where name like`%Zs%`;
    ```

