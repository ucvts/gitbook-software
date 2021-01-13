# Establishing a Connection

## Connect

Establishing a connection to your database is a critical first step to writing a database-drive application of any type. This process is fairly straightforward, but can be intimidating and frustrating if you've never worked with a database system before.

It'll vary based on the languages and database technologies you're using, but here's a rough approximation of the steps you'll need to follow. I'll highlight dialect-specific nuances as they arise in later tutorials and projects.

Let's take a look at a few examples.

```java
Properties props = new Properties();
        
// we need to add user and password properties to the
// connection string to authenticate
        
props.put("user", "myUsername");
props.put("password", "myPassword");
        
// jdbc:derby is the protocol the driver uses, so it'll need
// to be part of every connection string. mySampleDatabaseName
// is the name of our database, and create=true means we'll
// create this database if it doesn't already exist.

Connection conn = DriverManager.getConnection(
    "jdbc:derby:mySampleDatabaseName;create=true",
    props
);
```

The example above uses an Apache Derby database, and the connection is made in Java. We're using a Properties object where we're adding the username and password, but these can be passed in directly to the `getConnection` method, too.

Most other database technologies would use a similar connection process. For MySQL, as an example, the process would be the same with the exception of the protocol. Apache Derby uses `jdbc:derby` as the protocol, whereas MySql uses `jdbc:mysql`. The protocol in use is determined by the driver, and is usually readily available in the the driver's online documentation.

Once we have a `Connection` object \(referenced by the variable `conn` in the example above\), we can issue SQL statements against the database. It is your responsibility as a programmer to close the `Connection` object when you're finished.

```java
conn.close();
```

