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