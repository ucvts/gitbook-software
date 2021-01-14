# Data Manipulation

## Querying Tables

Data manipulation is the meat and potatoes of using SQL in applications. We've gone over data definition, which pertains to creating, altering, and dropping databases and tables. Data manipulation, on the other hand, pertains to querying, inserting, updating, and deleting information.

To query a table, we can issue a `SELECT` statement against it. Suppose we have the following table \(called `students`\).

| id | name | street | city | state | postal |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Patrick Smith | 123 Main Street | Scotch Plains | NJ | 07076 |
| 2 | Samantha Jones | 789 First Avenue | Scotch Plains | NJ | 07076 |
| 3 | Ryan Wilson | 456 Lake Avenue | Rahway | NJ | 07065 |

We can choose any number of columns from this table. Maybe we only want to grab the names and cities of every person in this table.

```sql
SELECT name, city FROM students;
```

We could also grab everything. All rows, all columns.

```sql
SELECT * FROM students;
```

If we needed to filter for a certain subset of data that met some condition, we'd use a `WHERE` clause.

```sql
SELECT name, city FROM students WHERE city = 'Rahway';
```

Our WHERE clause would match only records whose `city` value was equal to `Rahway`. This is just the tip of the iceberg, and I encourage you to explore much more deeply. You can find just about anything on the Internet. Here's a [push in the right direction](https://www.codecademy.com/learn/learn-sql).

## Inserting Data

If we can extract data from a table, then naturally there needs to be a way to put data into it, too. The `INSERT` statement does just that.

You provide the table and columns you're inserting into, followed by the values for each column. This depends on the rules setup during the creation of your table \(e.g., which columns can or can't be `null`, etc.\), but here's a pretty simply example.

```sql
INSERT INTO students (
   name,
   street,
   city,
   state,
   postal
) VALUES (
   'Amy Strickenberger',
   '12 Schoolhouse Road',
   'Elizabeth',
   'NJ',
   '07114'
);
```

Each value in the `VALUES` list corresponds to a column in the insert list. I've left off the `id` column, which we'll imagine is an auto-incrementing primary key. You don't need to provide an explicit value for these types of columns, as they are generating automatically on each insertion.

## Modifying Data

Next up is changing data. Maybe Patrick Smith moves to Union, NJ. We'll need to update his record in the table. We need to make sure our change affects only Patrick's record, and we'll do that by using the primary key.

A primary key is a value or set of values that guarantees the uniqueness of a record. The `id` column is the primary key for the `students` table. We need to update the `street`, `city`, and `postal` columns. Everything can remain unchanged.

```sql
UPDATE students SET
   street = '7 Cranberry Lane',
   city = 'Union',
   postal = '07033'
WHERE id = 1;
```

We're using the familiar `WHERE` clause to target a specific record.

We can do the same thing if we need to delete a record. Perhaps they've restructured the boundaries of Union County, and Rahway got the boot. Those students need to transfer to another county vocational school. We can remove these records from the table with a `DELETE` statement.

```sql
DELETE FROM students WHERE city = 'Rahway';
```

Every records whose `city` value equals `Rahway` will be purged from the table. Be careful with these statements, as they can quickly wipe out a huge amount of data.

