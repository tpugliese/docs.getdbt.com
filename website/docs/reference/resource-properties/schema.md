---
resource_types: sources
datatype: schema_name
---

<File name='models/<filename>.yml'>

```yml
version: 2

sources:
  - name: <source_name>
    database: <database_name>
    schema: <schema_name>
    tables:
      - name: <table_name>
      - ...

```

</File>

## Definition
The schema name as stored in the database.

This parameter is useful if you want to use a source name that differs from the schema name.

<Alert type='info'>

#### BigQuery terminology
If you're using BigQuery, use the _dataset_ name as the `schema:` property.

</Alert>

## Default
By default, dbt will use the source's `name:` parameter as the schema name.

## Examples
### Use a simpler name for a source table than the one in your database

<File name='models/<filename>.yml'>

```yml
version: 2

sources:
  - name: jaffle_shop
    tables:
      - name: orders
        identifier: api_orders


```

</File>


In a downstream model:
```sql
select * from {{ source('jaffle_shop', 'orders') }}
```

Will get compiled to:

```sql
select * from jaffle_shop.api_orders
```
