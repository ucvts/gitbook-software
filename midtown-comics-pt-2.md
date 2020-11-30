# Midtown Comics, Pt. 2

## Summary

Software engineers are sometimes tasked with creating brand new products from scratch. More often than not, though, they're asked to maintain and enhance existing products. And that's exactly what we \(and you!\) are going to do.

The Midtown Comics point-of-sale is already up-and-running, but it leaves much to be desired. We're going to enhance the application to use a backend database to store products, customers, and orders. We'll tackle everything related to products together, and it'll be up to you to write the code for customers and orders. You can always use the code we write together as a template for your own code.

## Creating the Database

First things first. If we're going to have a database, we'll need to write the SQL to create it. This might ordinarily live in a `.sql` file, but we'll keep things a little more simple and write a Java class for it.

The class is pretty heavily commented, so do yourself a favor and read through them.

{% code title="SetupDao.java" %}
```java
package org.ucvts.comics.dao;

import java.sql.Connection;
import java.sql.DatabaseMetaData;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

public class DAO {
        
    private static Connection conn;            // a connection to the database
    private static DatabaseMetaData metadata;  // a reference to the database metadata
    
    /**
     * Creates each table in the database, inserting sample records when
     * and where applicable.
     * 
     * @throws SQLException
     */
    
    public static void buildDatabase() throws SQLException {
        conn = DAO.getConnection();
        metadata = conn.getMetaData();
        
        DAO.createProductsTable();      // creates products table
        DAO.createCustomersTable();     // creates customers table
        DAO.createOrdersTable();        // creates orders table
        DAO.createOrderItemsTable();    // creates orderitems table
                
        conn.close();
    }
    
    /*
     * Creates the products table if it doesn't already exist.
     * 
     * @throws SQLException
     */
    
    private static void createProductsTable() throws SQLException {
        ResultSet rs = metadata.getTables(null, "USER1", "PRODUCTS", null);
        
        // getTables returns any tables named products. if next returns
        // false, then we haven't yet created the products table. we'll
        // do so now.
        
        if (!rs.next()) {
            Statement stmt = conn.createStatement();
            
            stmt.execute(
                "CREATE TABLE products (" +
                "   id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY (START WITH 1, INCREMENT BY 1), " +
                "   title VARCHAR(128) NOT NULL, " +
                "   author VARCHAR(64) NOT NULL, " +
                "   releasedate BIGINT NOT NULL, " +
                "   issue INT NOT NULL, " +
                "   unitprice DECIMAL(10, 2) NOT NULL, " +
                "   copies INT NOT NULL" +
                ")"
            );
            
            // we're going to insert the same sample products we used in
            // the Midtown Comics, Pt. 1 tutorial. this time, they'll be
            // in a database instead of in memory (in an ArrayList).
            
            insertSampleProducts();
        }
    }
    
    /*
     * Creates the customers table if it doesn't already exist.
     * 
     * @throws SQLException
     */
    
    private static void createCustomersTable() throws SQLException {
        ResultSet rs = metadata.getTables(null, "USER1", "CUSTOMERS", null);
        
        // getTables returns any tables named customers. if next returns
        // false, then we haven't yet created the customers table. we'll
        // do so now.
                
        if (!rs.next()) {
            Statement stmt = conn.createStatement();
            
            stmt.execute(
                "CREATE TABLE customers (" +
                "   id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY (START WITH 1, INCREMENT BY 1), " +
                "   firstname VARCHAR(64) NOT NULL, " +
                "   lastname VARCHAR(64) NOT NULL, " +
                "   phone BIGINT NOT NULL, " +
                "   email VARCHAR(255) NOT NULL, " +
                "   street VARCHAR(255) NOT NULL, " +
                "   city VARCHAR(255) NOT NULL, " +
                "   state CHAR(2) NOT NULL, " +
                "   postalcode CHAR(5) NOT NULL" +
                ")"
            );
        }
    }
    
    /*
     * Creates the orders table if it doesn't already exist.
     * 
     * @throws SQLException
     */
    
    public static void createOrdersTable() throws SQLException {
        ResultSet rs = metadata.getTables(null, "USER1", "ORDERS", null);
        
        // getTables returns any tables named orders. if next returns
        // false, then we haven't yet created the orders table. we'll
        // do so now.
                
        if (!rs.next()) {
            Statement stmt = conn.createStatement();
            
            stmt.execute(
                "CREATE TABLE orders (" +
                "   id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY (START WITH 1, INCREMENT BY 1), " +
                "   orderdate BIGINT NOT NULL, " +
                "   status CHAR(1) NOT NULL, " +
                "   total DECIMAL(20, 2) NOT NULL, " +
                "   customerid BIGINT references customers(id)" +
                ")"
            );
        }
    }
    
    /*
     * Creates the orderitems table if it doesn't already exist.
     * 
     * @throws SQLException
     */
    
    public static void createOrderItemsTable() throws SQLException {
        ResultSet rs = metadata.getTables(null, "USER1", "ORDERITEMS", null);
        
        // getTables returns any tables named orderitems. if next returns
        // false, then we haven't yet created the orderitems table. we'll
        // do so now.
                
        if (!rs.next()) {
            Statement stmt = conn.createStatement();
            
            stmt.execute(
                "CREATE TABLE orderitems (" +
                "   id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY (START WITH 1, INCREMENT BY 1), " +
                "   quantity BIGINT NOT NULL, " +
                "   orderid BIGINT references orders(id), " +
                "   productid BIGINT references products(id)" +
                ")"
            );
        }
    }
    
    /*
     * Inserts sample records into the products table.
     * 
     * @throws SQLException
     */
    
    private static void insertSampleProducts() throws SQLException {
        Statement stmt = conn.createStatement();
        
        // this will serve as our initial inventory of products
        
        stmt.executeUpdate("INSERT INTO products (title, author, releasedate, issue, unitprice, copies) VALUES ('The Amazing Spider-Man', 'Stan Lee', 19630301, 1, 19.99, 3)");
        stmt.executeUpdate("INSERT INTO products (title, author, releasedate, issue, unitprice, copies) VALUES ('The Amazing Spider-Man', 'Stan Lee', 19630510, 2, 19.99, 7)");
        stmt.executeUpdate("INSERT INTO products (title, author, releasedate, issue, unitprice, copies) VALUES ('The Amazing Spider-Man', 'Stan Lee', 19630710, 3, 19.99, 9)");
        stmt.executeUpdate("INSERT INTO products (title, author, releasedate, issue, unitprice, copies) VALUES ('The Amazing Spider-Man', 'Stan Lee', 19630910, 4, 19.99, 12)");
        stmt.executeUpdate("INSERT INTO products (title, author, releasedate, issue, unitprice, copies) VALUES ('The Amazing Spider-Man', 'Stan Lee', 19631010, 5, 19.99, 3)");
        stmt.executeUpdate("INSERT INTO products (title, author, releasedate, issue, unitprice, copies) VALUES ('The Amazing Spider-Man', 'Stan Lee', 19631110, 6, 19.99, 7)");
        stmt.executeUpdate("INSERT INTO products (title, author, releasedate, issue, unitprice, copies) VALUES ('The Amazing Spider-Man', 'Stan Lee', 19631210, 7, 19.99, 9)");
        stmt.executeUpdate("INSERT INTO products (title, author, releasedate, issue, unitprice, copies) VALUES ('The Amazing Spider-Man', 'Stan Lee', 19640110, 8, 19.99, 12)");
        stmt.executeUpdate("INSERT INTO products (title, author, releasedate, issue, unitprice, copies) VALUES ('The Amazing Spider-Man', 'Stan Lee', 19640210, 9, 19.99, 3)");
        stmt.executeUpdate("INSERT INTO products (title, author, releasedate, issue, unitprice, copies) VALUES ('The Amazing Spider-Man', 'Stan Lee', 19640310, 10, 19.99, 7)");
        
        stmt.close();
    }
    
    /*
     * Establishes and returns a connection to the database.
     * 
     * @return a connection to the database
     * @throws SQLException
     */
    
    private static Connection getConnection() throws SQLException {
        Properties props = new Properties();
        
        // we need to add user and password properties to the
        // connection string to authenticate
        
        props.put("user", "user1");
        props.put("password", "user1");
        
        // jdbc:derby is the protocol the driver uses, so it'll need
        // to be part of every connection string. midtowncomics is the
        // name of our database, and create=true means we'll create
        // this database if it doesn't already exist.

        return DriverManager.getConnection("jdbc:derby:midtowncomicsdb;create=true", props);
    }
}
```
{% endcode %}

There's only one public method in this class: `buildDatabase`. It creates a connection, grabs the metadata for that connection, and then calls a series of private methods.

* `createProductsTable`
* `createCustomersTable`
* `createOrdersTable`
* `createOrderItemsTable`

These should ring a bell. Each table represents a model object from the [Midtown Comics, Pt. 1](midtown-comics-pt-1.md) tutorial. They all work the same way, so we'll use `createProductsTable` as an example.

This code will be called from our `ViewManager`, but we only want to create these tables once. We need to use the connection metadata to see if the table already exists. If it doesn't we'll create it.

```java
ResultSet rs = metadata.getTables(null, "USER1", "PRODUCTS", null);

if (!rs.next()) {
    // the products table doesn't exist, we need to create it
}
```

If the result set that is returned from `getTables` contains a row, then the `products` table exists. If it doesn't, we run the create statement. We're inserting sample records here, but that won't be necessary for the `customers`, `orders`, or `orderitems` tables.

Now, we need to modify the `ViewManager` to trigger the database code.

```java
package org.ucvts.comics.controller;

import java.awt.CardLayout;
import java.awt.Container;
import java.sql.SQLException;
import java.util.List;

import org.ucvts.comics.MidtownComics;
import org.ucvts.comics.dao.DAO;
import org.ucvts.comics.model.Order;
import org.ucvts.comics.model.OrderItem;
import org.ucvts.comics.model.Product;
import org.ucvts.comics.view.CartView;
import org.ucvts.comics.view.InventoryView;
import org.ucvts.comics.view.OrderView;
import org.ucvts.comics.view.ProductView;

public class ViewManager {

    private static ViewManager manager;

    private Container views;
    private Order order;
    
    /*
     * A private constructor, implementing the singleton pattern.
     * 
     * @param views
     */

    private ViewManager(Container views) {
        this.views = views;
        
        // rudimentary error handling. a more mature application
        // would handle database exceptions more gracefully, but
        // we'll just print the stack trace for now.
        
        try {
            DAO.buildDatabase();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    // remaining methods not shown   
}
```

So far, so good. Our database is created, and we've got some sample records in the `products` table. Now, we need another class that deals specifically with product-related database interactions.

