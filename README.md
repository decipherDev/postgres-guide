## Basic Commands
#### Setting the search path to a schema in postgres

```SET SEARCH_PATH = <schema-name>;```

#### Searching for tables from all schemas

```SELECT * FROM pg_tables WHERE tablename = ''```

#### Searching for columns with table names from all schemas

```SELECT * FROM information_schema.columns WHERE column_name = ''```

#### To use buit-in pgstattuple extension

```CREATE EXTENSION pgstattuple;```

#### To analyse a table for fragmentation

```SELECT * FROM pgstattuple('table_name');```

#### To analyse an index for fragmentation

```SELECT * FROM pgstatindex('index_name');```
  
## Paritioning by range

```
  CREATE TABLE EMPLOYEE (
  empId INTEGER,
  name TEXT NOT NULL,
  dept TEXT NOT NULL,
  dateOfJoining date
) PARTITION BY RANGE (dateOfJoining);

CREATE TABLE EMPLOYEE_2024 PARTITION OF EMPLOYEE FOR VALUES FROM ('2024-01-01') TO ('2024-12-31');
CREATE TABLE EMPLOYEE_2023 PARTITION OF EMPLOYEE FOR VALUES FROM ('2023-01-01') TO ('2023-12-31');

-- -- insert
INSERT INTO EMPLOYEE VALUES (0001, 'Clark', 'Sales', CURRENT_DATE-1);
INSERT INTO EMPLOYEE VALUES (0002, 'Dave', 'Accounting', CURRENT_DATE-2);
INSERT INTO EMPLOYEE VALUES (0003, 'Ava', 'Sales', CURRENT_DATE-3);
INSERT INTO EMPLOYEE VALUES (0004, 'AvaB', 'Sales', CURRENT_DATE-365);
```
