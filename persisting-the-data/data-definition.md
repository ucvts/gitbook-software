# Data Definition

## Working with Databases

One of the biggest concerns in software development is data. It sparks a number of questions that need to be considered in the planning and design stages of a project.

* How much data will our application process?
* What will the types and formats of the data be?
* How and where should we store this data?

Enter, databases. Just about every application you use today has one \(or many\), from games you play online to apps you use on your phone or tablet. When we think about interacting with databases, we break down the means of communication into two primary languages.

* Data definition language \(DDL\), which is used to create or alter the structure of a database.
* Data manipulation language \(DML\), which is used to modify the contents of a database.

We're going to start with DDL before jumping into connecting to and manipulating a database.

## Relational Model

There are a number of different models of databases in use today. We're going to work with a traditional relational database. In this model, the database contains tables that represent an entity in your application. Each table, in turn, stores rows corresponding to individual records.

## Create

Create statements are where it all begins. You need to create a database, and then create tables in that database before you can do anything else.

### Create a Database

```sql
CREATE DATABASE databasename;
```

### Creating a Table

Table creation is a little more complicated. The exact syntax would depend on the vendor you're using, but here's the general idea.

```sql
CREATE TABLE tablename (
    columnname1 datatype,
    columnname2 datatype,
    columnname3 datatype
);
```

We'll get into the specifics in some later tutorials.

## Alter

Alterations are when you need to change an existing table structure. You might want to add a new column, remove an existing one, or edit the definition itself.

### Adding a Column

```sql
ALTER TABLE tablename
ADD columnname datatype;
```

### Dropping a Column

```sql
ALTER TABLE tablename
DROP columnname;
```

### Modifying a Column

```sql
ALTER TABLE tablename
MODIFY columnname datatype;
```

Again, the syntax is often vendor-specific. We'll cover this later.

## Drop

We've seen the drop syntax in relation to columns. It can also be used for tables and databases.

### Dropping a Database

```sql
DROP DATABASE databasename;
```

### Dropping a Table

```sql
DROP TABLE tablename;
```

