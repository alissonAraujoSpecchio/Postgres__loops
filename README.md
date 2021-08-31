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
or

```sql
DECLARE
    v_all_tables text[];
BEGIN
    SELECT array_agg(table_name) INTO v_all_tables FROM information_schema.tables WHERE table_schema = 'public';
    FOR i IN 1..array_length(v_all_tables, 1) LOOP
        raise notice 'table name - %', v_all_tables[i];
    END LOOP;
END;
```

## Loop in jsonb[] (jsonb array)
It works in json[] too, just use json instead of jsonb in the functions.

```sql
DECLARE
    v_json jsonb;
BEGIN
    SELECT jsonb_agg(column) INTO v_json FROM table WHERE condition;
    FOR i IN 0..jsonb_array_length(v_json)-1 LOOP
        raise notice '%', v_json->i;
    END LOOP;
END;
```
_Obs: Jsonb_agg creates a jsonb[]_

