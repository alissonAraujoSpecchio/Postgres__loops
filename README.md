# Postgres__loops

## Loop in text[] (text array)

```sql
DECLARE
    v_all_tables text[];
    v_table_name text;
BEGIN
    SELECT array_agg(table_name) INTO v_all_tables FROM information_schema.tables WHERE table_schema = 'public';
    FOREACH v_table_name IN ARRAY v_all_tables LOOP
        raise notice 'table name - %', v_table_name;
    END LOOP;
END;
```
