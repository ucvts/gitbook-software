# Midtown Comics, Pt. 2

## Summary

Software engineers are sometimes tasked with creating brand new products from scratch. More often than not, though, they're asked to maintain and enhance existing products. And that's exactly what we \(and you!\) are going to do.

The Midtown Comics point-of-sale is already up-and-running, but it leaves much to be desired. We're going to enhance the application to use a backend database to store products, customers, and orders. We'll tackle everything related to products together, and it'll be up to you to write the code for customers and orders. You can always use the code we write together as a template for your own code.

## Creating the Database

First things first. If we're going to have a database, we'll need to write the SQL to create it. This might ordinarily live in a `.sql` file, but we'll keep things a little more simple and write a Java class for it.

The class is pretty heavily commented, so do yourself a favor and read through them.

{% code title="DAO.java" %}
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
    
    static Connection getConnection() throws SQLException {
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
import java.util.ArrayList;
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
     * The singleton pattern guarantees that only a single instance
     * of the ViewManager class will every be instantiated.
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

## Data Access

There are four simple operations we'll need to support, one of which will be broken into two methods.

* Retrievals
* Insertions
* Updates
* Deletions

Again, it's heavily documented. Read the comments!

{% code title="ProductDAO.java" %}
```java
package org.ucvts.comics.dao;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;

import org.ucvts.comics.model.Product;

public class ProductDAO {

    /**
     * Retrieves a Product from the database.
     * 
     * @param productId the productId of the product to retrieve
     * @return the product retrieved from the database
     * @throws SQLException 
     */
    
    public static Product getProduct(long productId) throws SQLException {
        Product product = null;
        
        // first, we need to establish a connection to the database. we
        // call getConnection, which will return a new connection object.
        
        Connection conn = DAO.getConnection();
        
        // a statement is a query we'll execute on the database. this
        // includes select, insert, update, and delete statements. a
        // prepared statement is a parameterized statement that allows
        // us to pass in values to predefined placeholders.
        
        PreparedStatement pstmt = conn.prepareStatement("SELECT * FROM products WHERE productId = ?");
        
        // we need to provide an actual value for our placeholder.
        
        pstmt.setLong(1, productId);
        
        // when we execute our query (a select statement), it's going to
        // return zero or more rows. we'll store that result in what is
        // called a result set.
        
        ResultSet rs = pstmt.executeQuery();
        
        // a result set has something called a cursor that points at the
        // current row. initially, this cursor is positioned before the
        // first row (i.e., it points at nothing). we need to call next
        // to tell the cursor to advance to the first row.
        //
        // next returns a boolean value. if it returns true, that means
        // the cursor successfully advanced to the next row (which, in this
        // case, is the first row).
        //
        // our query is designed to return a single row. if next returns
        // true, that means we've got a row. we'll use that row to build
        // a product object.
            
        if (rs.next()) {
            product = new Product();
            
            product.setProductId(rs.getLong(1));
            product.setTitle(rs.getString(2));
            product.setAuthor(rs.getString(3));
            product.setReleaseDate(rs.getLong(4));
            product.setIssue(rs.getInt(5));
            product.setUnitPrice(rs.getDouble(6));
            product.setCopies(rs.getInt(7));
        }
        
        // we're done with the result set, prepared statement, and connection
        // objects, so we should close them. this is a form of memory management.
                
        rs.close();
        pstmt.close();
        conn.close();
        
        return product;
    }
    
    /**
     * Retrieves all Products from the database.
     * 
     * @return a list of products retrieved from the database
     * @throws SQLException
     */
    
    public static List<Product> getProducts() throws SQLException {
        List<Product> products = new ArrayList<>();
        Connection conn = DAO.getConnection();
        
        // earlier, we created a prepared statement (i.e., a parameterized
        // statement). this is just a regular statement, which is used for
        // simpler queries that don't require additional values.
        
        Statement stmt = conn.createStatement();
        
        // statements are executed the same way prepared statements are. their
        // results are stored in a result set, too. the only difference is we
        // pass the SQL directly into the executeQuery method.
        
        ResultSet rs = stmt.executeQuery("SELECT * FROM products");
        
        // remember, next returns true if the cursor is advanced to the next
        // row. last time, we called next in an if statement to advance the
        // cursor to the first and only row.
        //
        // this query is designed to return more than one row, so we call next
        // in the condition of a while loop instead. this allows us to repeatedly
        // build products from every row in the result set. the while loop will
        // exist after the last row is processed and next returns false.
                
        while (rs.next()) {
            Product product = new Product();
            
            product.setProductId(rs.getLong(1));
            product.setTitle(rs.getString(2));
            product.setAuthor(rs.getString(3));
            product.setReleaseDate(rs.getLong(4));
            product.setIssue(rs.getInt(5));
            product.setUnitPrice(rs.getDouble(6));
            product.setCopies(rs.getInt(7));
                        
            products.add(product);
        }
        
        rs.close();
        stmt.close();
        conn.close();
        
        return products;
    }
    
    /**
     * Inserts a Product into the database.
     * 
     * @param product the product to insert into the database
     * @throws SQLException
     */
        
    public static void insertProduct(Product product) throws SQLException {        
        Connection conn = DAO.getConnection();        
        PreparedStatement pstmt = conn.prepareStatement(
            "INSERT INTO products (" +
            "   title, " +
            "   author, " +
            "   releasedate, " +
            "   issue, " +
            "   unitprice, " +
            "   copies " +
            ") VALUES (?, ?, ?, ?, ?, ?)"
        );
        
        // we've got quite a few more placeholders to fill in this time. they
        // are numbered in the order in which they appear in the SQL statement.
        
        pstmt.setString(1, product.getTitle());
        pstmt.setString(2, product.getAuthor());
        pstmt.setLong(3, product.getReleaseDate());
        pstmt.setInt(4, product.getIssue());
        pstmt.setDouble(5, product.getUnitPrice());
        pstmt.setInt(6, product.getCopies());
        
        pstmt.executeUpdate();
        pstmt.close();
        conn.close();
    }
    
    /**
     * Updates an existing Product in the database
     * 
     * @param product the new product used to update the old one
     * @throws SQLException
     */
    
    public static void updateProduct(Product product) throws SQLException {
        Connection conn = DAO.getConnection();
        PreparedStatement pstmt = conn.prepareStatement(
            "UPDATE products SET " +
            "   title = ?, " +
            "   author = ?, " +
            "   releasedate = ?, " +
            "   issue = ?, " +
            "   unitprice = ?, " +
            "   copies = ? " +
            "WHERE id = ?"
        );
                
        pstmt.setString(1, product.getTitle());
        pstmt.setString(2, product.getAuthor());
        pstmt.setLong(3, product.getReleaseDate());
        pstmt.setInt(4, product.getIssue());
        pstmt.setDouble(5, product.getUnitPrice());
        pstmt.setInt(6, product.getCopies());
        pstmt.setLong(7, product.getProductId());
        
        pstmt.executeUpdate();
        pstmt.close();
        conn.close();
    }
    
    /**
     * Deletes an existing Product from the database.
     * 
     * @param product the product to delete
     * @throws SQLException
     */
    
    public static void deleteProduct(Product product) throws SQLException {
        Connection conn = DAO.getConnection();
        PreparedStatement pstmt = conn.prepareStatement("DELETE FROM products WHERE id = ?");
        
        // we're deleting a product from the table, so we only need the primary key
        // (in this case, the id column). a primary key, which can be a combination
        // of columns (called a composite key) is the value that is guaranteed to
        // uniquely identify a row in the table.
        
        pstmt.setLong(1, product.getProductId());
        
        pstmt.executeUpdate();
        pstmt.close();
        conn.close();
    }
}

```
{% endcode %}

Alright, let's revisit the ViewManager class. We'll need to make a few more changes to start interacting with the `ProductDAO` class. DAO, by the way, stands for data access object. It's a fancy way of saying this object will be used to access data \(for the `Product` class, in this case\).

It's easier to include the entire `ViewManager` class here, but the comments flag the lines of code that are new versus those that are unchanged.

{% code title="ViewManager.java" %}
```java
package org.ucvts.comics.controller;

import java.awt.CardLayout;
import java.awt.Container;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;

import org.ucvts.comics.MidtownComics;
import org.ucvts.comics.dao.DAO;        // this is a new import statement
import org.ucvts.comics.dao.ProductDAO; // this is a new import statement
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
     * The singleton pattern guarantees that only a single instance
     * of the ViewManager class will every be instantiated.
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
    
    /**
     * Returns an instance of the ViewManager class, creating one if necessary.
     * 
     * @param views the parent container
     * @return an instance of the ViewManager class
     */

    public static ViewManager getInstance(Container views) {
        if (manager == null) {
            manager = new ViewManager(views);
        }

        return manager;
    }
    
    /**
     * Switches to the specified named view.
     * 
     * @param view the view to switch to
     */

    public void switchTo(String view) {
        ((CardLayout) views.getLayout()).show(views, view);
    }
    
    /**
     * Attaches a product to the product view.
     * 
     * @param product the product to attach
     */
    
    public void attachProduct(Product product) {
        ((ProductView) views.getComponent(MidtownComics.ProductViewIndex)).setProduct(product);
    }
    
    /**
     * Detaches a product from the product view.
     */
    
    public void detachProduct() {
        ((ProductView) views.getComponent(MidtownComics.ProductViewIndex)).setProduct(null);
    }
    
    /**
     * Adds a new Product to inventory.
     * 
     * @param product the new product
     */

    public void addProductToInventory(Product product) {
        try {            
            ProductDAO.insertProduct(product);  // this is new, add product to the database
    
            detachProduct();
            refreshInventoryList();
            switchTo(MidtownComics.InventoryView);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    /**
     * Modifies an existing Product in inventory.
     * 
     * @param product the modified product
     */

    public void modifyProductInInventory(Product product) {
        try {
            ProductDAO.updateProduct(product);  // this is new, updates product in the database
            
            detachProduct();
            refreshInventoryList();
            switchTo(MidtownComics.InventoryView);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    /**
     * Removes an existing Product from inventory.
     * 
     * @param product the product to be removed
     */

    public void removeProductFromInventory(Product product) {
        try {
            ProductDAO.deleteProduct(product);  // this is new, deletes product from the database
    
            detachProduct();
            refreshInventoryList();
            switchTo(MidtownComics.InventoryView);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    /**
     * Adds an OrderItem to an Order, creating the Order first if necessary.
     * 
     * @param item the item to be added
     */

    public void addItemToOrder(OrderItem item) {
        if (order == null) {
            order = new Order();
        }

        order.addItem(item);
        refreshCart();
        updateOrderTotal();
        manager.switchTo(MidtownComics.CartView);
    }

    /**
     * Modify the quantity of an OrderItem in an Order.
     * 
     * @param product  the product to be modified
     * @param quantity the new quantity
     */

    public void modifyItemQuantityInOrder(Product product, int quantity) {
        int index = findItemInOrder(product);
        order.getItems().get(index).setQuantity(quantity);        

        refreshCart();
        updateOrderTotal();
        switchTo(MidtownComics.InventoryView);
        switchTo(MidtownComics.CartView);
    }

    /**
     * Remove an OrderItem from an existing Order.
     * 
     * @param product the product to be removed
     */

    public void removeItemFromOrder(Product product) {
        int index = findItemInOrder(product);
        order.getItems().remove(index);

        refreshCart();
        updateOrderTotal();
        switchTo(MidtownComics.InventoryView);
        
        if (order.getItems().size() > 0) {
            switchTo(MidtownComics.CartView);
        }
    }
    
    /**
     * Returns the OrderItem quantity by Product.
     * 
     * @param product the product whose quantity we need
     * @return the order item quantity
     */
    
    public int getOrderItemQuantity(Product product) {
        int index = findItemInOrder(product);
        
        return index != -1 ? order.getItems().get(index).getQuantity() : 0;
    }
    
    /**
     * Returns the subtotal for this Product.
     * 
     * @param product the product whose subtotal we need
     * @return the subtotal
     */
    
    public double getSubtotal(Product product) {
        int index = findItemInOrder(product);
        
        return index != -1 ? order.getItems().get(index).getPrice() : 0;
    }
    
    /**
     * Returns whether or not the Product already exists in the Order.
     * 
     * @param product the product
     * @return whether or not it exists in the order
     */
    
    public boolean productExistsInOrder(Product product) {
        if (order == null) {
            return false;
        }
        
        return findItemInOrder(product) != -1;
    }
    
    /**
     * Submits an order. Aside from updating the inventory, this
     * is all for show. We'll change that later.
     * 
     * @throws SQLException
     */
    
    public void submitOrder() throws SQLException {
        for (int i = 0; i < order.getItems().size(); i++) {
            OrderItem item = order.getItems().get(i);
            Product product = item.getProduct();
            int quantity = item.getQuantity();
            int copies = product.getCopies();
            
            product.setCopies(copies - quantity);
            modifyProductInInventory(product);
        }
        
        order = null;
        clearOrder();
    }

    /**
     * Retrieves the inventory.
     * 
     * @return the inventory
     */
    
    public List<Product> getInventory() {
        try {
            return ProductDAO.getProducts();    // this is new, retrieves all products from the database
        } catch (SQLException e) {
            e.printStackTrace();
        }
        
        return new ArrayList<>();
    }
    
    /**
     * Retrieves the current order.
     * 
     * @return the current order
     */
    
    public Order getOrder() {
        return order;
    }

    /*
     * Refreshes the inventory list in the InventoryView.
     */
    
    private void refreshInventoryList() {
        ((InventoryView) views.getComponent(MidtownComics.InventoryViewIndex)).refreshInventoryList();
    }
    
    /*
     * Refreshes the cart in the CartView.
     */
    
    private void refreshCart() {
        ((CartView) views.getComponent(MidtownComics.CartViewIndex)).refreshCart();
    }
    
    /*
     * Updates the order total in the OrderView.
     */
    
    private void updateOrderTotal() {
        ((OrderView) views.getComponent(MidtownComics.OrderViewIndex)).updateOrderTotal(order.getTotal());
    }
    
    /*
     * Clears the current order in the OrverView.
     */
    
    private void clearOrder() {
        ((OrderView) views.getComponent(MidtownComics.OrderViewIndex)).clearOrder();
    }

    /*
     * Finds an OrderItem in an Order.
     * 
     * @param product the product we're looking for
     * @return the index of the item in the order
     */
    
    private int findItemInOrder(Product product) {
        for (int i = 0; i < order.getItems().size(); i++) {
            if (order.getItems().get(i).getProduct().getProductId() == product.getProductId()) {
                return i;
            }
        }

        return -1;
    }
}
```
{% endcode %}

Now, we've get everything in place to use the application as it were with a database backend. If you add products, or edit or remove existing ones, you can close the application and restart it and the changes will persist.

## Enhancements

After completing the tutorial, you'll be tasked with making a couple enhancements to this application. We've setup the backend for orders and customers, but we're not really doing anything with them in the UI. Time to change that.

### Customer Information

Build out a DAO for customers \(similar to the `ProductDAO` class\) that will allow you to do the following.

1. Retrieve a single customer from the database by ID.
2. Retrieve all customers from the database.
3. Insert a single customer into the database.
4. Update a single customer in the database.
5. Delete a single customer from the database.

Once you've got the backend wired up, build a  view called `CustomerListView`. It should mimic the `InventoryView`, in that it provides a UI for viewing, editing, adding, or deleting customers.

### Order Information

Build out a DAO for orders \(including their items\) that will allow you to do the following.

1. Retrieve a single order \(including all items\) from the database by ID.
2. Retrieve all orders \(including all items\) from the database.
3. Insert a single order \(with one or more items\) into the database.
4. Update a single order \(including any items\) in the database.
5. Delete a single order \(including all items\) from the database. 

Once you've got the backend wired up, build a view called `OrderListView`. It should mimic the `InventoryView`, in that it provides a UI for viewing, editing, or deleting orders \(and their items\).

## Deliverables

1. Submit your repository URL.
2. Submit a video demo for the tutorial + enhancements \(between 3 and 5 minutes\).

Follow the tutorial and implement a working Midtown Comics application with a database. It should match mine in every way. From there, your code will diverge from that of the tutorial as you implement the enhancements.

Your video demo must show the working tutorial, including the ability to close and reopen the program to see persisted changes. Of course, it should also show the `CustomerListView` and `OrderListView` enhancements \(the views and functionalities\).

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, December 13, 2020.

