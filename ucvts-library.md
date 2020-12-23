# UCVTS Library

## Summary

Ideally, we would've gotten to this sooner than December; however, with the course sequence a bit out of whack this year, it was helpful to gain a bit more experience in Java before jumping into web applications.

Before we begin, we'll need to configure our development environment. We're going to create an online system for managing library books, and we need more support than Java SE provides.

In just a few short weeks, you're going to gain some exposure to quite a few new technologies.

* Apache Tomcat
* Java Enterprise Edition \(Java EE\)
* MySQL
* Maven
* Java Database Connectivity \(JDBC\)
* Java Servlets & Java Server Pages \(JSP\)
* JSP Standard Tag Library \(JSTL\)

Don't worry, we're going to walk through it together. On to the configuration steps!

## Getting the Java EE Perspective

Java EE is the enterprise edition of the Java platform. It's what professional software developers use to create secure, multi-tiered, scalable web applications.

Eclipse has different perspectives tailored to the types of programs you're writing. We've been working with the standard edition thus far, so Eclipse has shown us the default Java SE perspective. To get the Java EE perspective, we need to download and install a few things.

Navigate to `Help > Install New Software...` to bring up the `Available Software` dialog box.

Type `http://download.eclipse.org/releases/<YOUR-VERSION-TAG>` in the `Work with` box. I am using Eclipse 2020-03, so my URL ends in `2020-12`. Yours may be different.

![Available Software](.gitbook/assets/install-software.png)

Expand the `Web, XML, Java EE and OSGi Enterprise Development` tree, and check the following components.

* `Eclipse Java EE Developer Tools`
* `Eclipse Java Web Developer Tools`
* `Eclipse Web Developer Tools`
* `JST Server Adapters`
* `JST Server Adapter Extensions`

If you're on a newer version of Eclipse, you might have access to a few more choices. You can select these components, too, if they're available.

* `Eclipse Java Web Developer Tools - JavaScript Support`
* `Eclipse Web JavaScript Developer Tools`
* `JavaScript Development Tools`

Click `Next >` a couple times, accept the license agreements, and click `Finish`. You'll be asked to restart Eclipse to complete the installation.

Locate the `Open Perspective` button in the top-right of the window. It's the one with the little plus sign, and it'll open a dialog where you can choose a new perspective.

![Choose a Perspective](.gitbook/assets/open-perspective.png)

Select `Java EE` and click `Open` to launch the perspective. It doesn't look a whole lot different, but it does offer the tools and technologies we'll need to build web applications.

![Java EE Perspective](.gitbook/assets/java-ee.png)

Most notably, you have a range of new types of projects you can create. For now, though, we're going to focus on the `Servers` tab towards the bottom of the window.

## Installing Tomcat

[Download the latest version of Tomcat](https://tomcat.apache.org/download-90.cgi) from the `Binary Distributions` section \(specifically, the Core subsection\). There are several options, so choose the one applicable to your operating system. If you need a little help, follow along with one of these walkthrough videos.

* [Installing Apache Tomcat on Windows](https://www.youtube.com/watch?v=QwExzQt0XGE)
* [Installing Apache Tomcat on macOS](https://wolfpaulus.com/tomcat/)

You can verify your Tomcat installation by navigating to `localhost:8080` \(assuming you stuck with the default port during installing\). If you see the Tomcat page, you're good to go.

![Apache Tomcat/9.0.35](.gitbook/assets/tomcat-page.png)

### Adding Tomcat to Eclipse

Select the `Servers` tab, which is where we'll add our Tomcat instance.

![Servers](.gitbook/assets/servers-tab.png)

Click the`No servers are available. Click this link to create a new server...` link to open the `New Server` dialog box. Open the `Apache` folder and select `Tomcat v9.0 Server,` which is what we installed earlier.

![Choose a Server](.gitbook/assets/new-server-1.png)

Click `Next >` and enter the installation directory. I installed Tomcat in `/usr/local/tomcat/apache-tomcat-9.0.35`, but your installation path will likely be different.

![Tomcat Installation Directory](.gitbook/assets/new-server-2.png)

Click Finish and you should see a new entry in your `Servers` tab.

![Tomcat v9.0 Server](.gitbook/assets/added-tomcat.png)

## Installing MySQL

First, you'll need to [download the MySQL Community Server](https://dev.mysql.com/downloads/mysql/). Just like with Tomcat, choose the appropriate download based on your OS. You'll have to login with your Oracle Web Account, which most of you probably created when you downloaded Java. If you don't have an Oracle Web Account, it's simple enough to create one.

Regardless of OS, you'll be taken through your typical click-through installer. You can keep the defaults as-is. If you're asked to create a password for the `root` user, make sure you remember it! The `root` user is how you'll login to your MySQL instance later.

Once the database is installed, we'll want an easier way to work with it. [Download the MySQL Workbench](https://www.mysql.com/products/workbench/), which will help us create, query, and visualize our tables.

![MySQL Workbench](.gitbook/assets/mysql.png)

## Creating a Project

Now, we're ready to create a new project. Go to `File > New > Dynamic Web Project`. Make sure your settings match mine. The rest of the tutorial will be based off this initial setup, so it can become confusing if your settings start to deviate from mine.

![Dynamic Web Project](.gitbook/assets/new-project.png)

Click `Finish` and the project will be added to your `Project Explorer`.

![Default Project](.gitbook/assets/project-created.png)

### Using Maven

Maven is a dependency management and build automation tool. Rather than manually include external libraries like we did in [Midtown Comics, Pt. 2](midtown-comics-pt-2.md), Maven will handle downloading and including any third-party libraries we'll need.

Right-click the project and click `Configure > Convert to Maven Project`. Make sure your settings match mine, including selecting a `Packaging` of `WAR`. Click `Finish` when you're ready.

![Convert to Maven](.gitbook/assets/maven.png)

After the project is converted to Maven, you should see a `pom.xml` file. There isn't much in it right now, but later we'll add our dependencies to this file.

![POM](.gitbook/assets/maven-pom.png)

#### Adding Dependencies

Remember, Maven is a dependency management tool. It automatically tracks and downloads external project dependencies. Let's start adding ours.

![Dependencies](.gitbook/assets/maven-dependencies.png)

I know that's a lot to type, and it's important that everything matches exactly. Normally, I want you to type everything out yourself. Just this once, though, you can copy and paste.

```markup
<project
  xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd"
>
  <modelVersion>4.0.0</modelVersion>
  <groupId>ucvts-library</groupId>
  <artifactId>ucvts-library</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>war</packaging>
  <name>ucvts-library</name>
  
  <dependencies>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>4.0.1</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>javax.servlet.jsp-api</artifactId>
      <version>2.3.3</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>jstl</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.22</version>
    </dependency>
  </dependencies>
</project>
```

Make sure the version numbers match between your `mysql` dependency and the version we downloaded earlier. The version on my machine is `8.0.22`, and my Maven dependency reflects this. Please verify your own MySQL version.

## Setting up the Database

Our database backs the entire application, so that's where we're going to start. These next few steps should be done in the MySQL Workbench.

First, we create the database and tell MySQL we'll be using it. Press the lightning bolt icon \(the one next to the save icon\) to execute both statements. The other lightning bolt icon will only execute the currently selected statement.

![Create Database](.gitbook/assets/create-database.png)

You should see the database appear in the `SCHEMAS` section.

![View Schema](.gitbook/assets/show-database.png)

Next, we'll create our one and only table: `books`.

![Create Table](.gitbook/assets/create-table.png)

This, too, will appear in the `SCHEMAS` section, though a refresh may be required.

![View Table](.gitbook/assets/table.png)

### Inserting Data

We'll insert some sample records into the `books` table so there's something to render.

![Insert Data](.gitbook/assets/insert-books.png)

We'll provide means by which users can add, remove, and modify data. For now, let's just make sure our data was inserted as expected. We'll do a quick `SELECT *` to view the entirety of the `books` table.

![Query Data](.gitbook/assets/select-books.png)

### Testing Connectivity

As we dive more deeply into this application, we'll do things much differently. These next few steps are meant to verify that our application is connecting to and reading data from our database.

Right-click the project in Eclipse and click `New > Class`. Click the `public static void main(String[] args)` checkbox to include a `main` method automatically.

![New Class](.gitbook/assets/new-class.png)

Let's wire up some quick code to make sure our application can talk to our database. We'll just read everything in our `books` table, and print it to the console.

![Demonstrate Connectivity](.gitbook/assets/test-connection.png)

Eclipse might ask you if you want to `Run on Server` or as a `Java Application`. For now, choose to run the program as a `Java Application`. Later, we'll work on the server side.

## Modeling the Data

Now that everything is wired up correctly, let's start writing some application-specific code. We'll start with a class to model the books in the database. Right-click the project and click `New > Class`. We'll be putting our `Book` class in a new package called `library`.

![Book Class](.gitbook/assets/book-class.png)

Let's add some code. We want to model the database entities, so we'll create an instance variable for each column in the `books` table.

* `id`
* `title`
* `author`
* `copies`
* `available`

We'll create a constructor using each of these fields, as well as some getters and setters. The `id`, `title`, and `author` never change, so we only need getters for those three. `copies` and `available` can change over time, so we'll need getters and setters for those two.

![Source Code for Book Class](.gitbook/assets/book-code.png)

### Creating the Data Access Layer

Now that we have a `Book` class to model books in the database, we need a class to provide the CRUD \(create, read, update, delete\) operations pertaining to a book. This is called a data access object.

Again, right-click the project and click `New > Class`. We'll call this class `BookDAO`, and we'll put it in the `library` package, too. A more complex project might make use of more packages, but the goal is to keep things simple for this tutorial.

![BookDAO Class](.gitbook/assets/bookdao-class.png)

We're going to put our JDBC methods in this class so we can use it to interact with the database. Let's take a minute to think about some of the interactions we'll want the ability to have.

* Retrieving a single book from the database
* Retrieving all books from the database
* Inserting a book into the database
* Updating a single book in the database
* Deleting a single book from the database

And obviously, we'll need the ability to connect to the database. So let's get programming.

First, we'll take a look at the general structure of the class, along with a private method for connecting to the database. All of our methods in this class will make use of the `getConnection` method.

![Source Code for BookDAO Class](.gitbook/assets/bookdao-code-1.png)

Next, we'll take a look at each method one by one. First up is `getBook`. This method retrieves a single book from the database using the given `id`.

![Source Code for BookDAO Class](.gitbook/assets/bookdao-code-2.png)

Similarly, we need a method for retrieving all of the books in the database. No `id` parameter is needed for `getBooks` because we aren't targeting a particular book.

![Source Code for BookDAO Class](.gitbook/assets/bookdao-code-3.png)

We'll use `insertBook` to add a book to the database. We need each component of a Book object to do this: `title`, `author`, `copies`, and `available`. The id is generated automatically by the database on insertions.

![Source Code for BookDAO Class](.gitbook/assets/bookdao-code-4.png)

We can make changes to existing books using `updateBook`. Just pass in the updated `book` object.

![Source Code for BookDAO Class](.gitbook/assets/bookdao-code-5.png)

And last but not least, we use `deleteBook` to remove a book from the database. Again, we'll pass in the existing `book` object to be removed.

![Source Code for BookDAO Class](.gitbook/assets/bookdao-code-6.png)

One point of emphasis that applies to each of these methods: `Connection`, `Statement`, `PreparedStatement`, and `ResultSet` objects need to be closed when you're done using them, and they should be closed in reverse order relative to their creation.

## Adding some JSP

Java Server Pages \(JSP\) represent the view of our application. These pages are responsible for displaying data in the browser. We're going to create a very simple one to show the books in our database.

Right-click the project and click `New > JSP File`. Select `WebContent` as the parent folder, and name the file `inventory.jsp`.

![Inventory JSP File](.gitbook/assets/inventory-jsp-1.png)

JSP files look a lot like HTML, but there are some important differences. We can use programming constructs that look a lot like Java to conditionally render information. Notice the special tags at the top? That's what allows us to run code inside our JSP files.

![Inventory JSP File](.gitbook/assets/inventory-jsp-2.png)

The second tag in this file denotes a `prefix`. We use that prefix to start all code blocks within our JSP file. See the `forEach` section? It starts with `<c:`, which tells JSP that we're about to run some Java code.

This file is pretty simple. It creates a table, loops through our collection of books, and renders them on the page. It's not fancy and there's very little styling, but it works.

## Creating the Servlet

The Java servlet will act as our controller, which routes requests and responses between the browser and our application. It's the most complicated part of the project, so we're going to start slow.

First, right-click the project and click `New > Class`. We're going to call this class `Controller`. We'll put this in the `application` package, and extend the `HttpServlet` class. You can browse for this in Eclipse during class creation.

![Creating a Servlet Class](.gitbook/assets/create-servlet.png)

At this point, we have our database, model \(`Book.java`\), and data access layer \(`BookDAO.java`\) created, and we just added `inventory.jsp`. Our servlet is what allows the JSP file to communicate with the data access later \(and by extension, the database\).

We'll add to this later. For now, we just want a proof-of-concept that we can access our database from the web and display its contents in the browser.

![Source Code for Servlet Class](.gitbook/assets/servlet-code.png)

The `doPost` and `doGet` methods are overridden from the `HttpServlet` class. They're responsible for accepting requests from the browser, processing them as needed, and sending responses back. Our `doGet` method does all the work here. It calls the `getBooks` method from the `BookDAO` class, and sends the list of books back to the browser.

Remember the `iventory.jsp` file? We setup a variable in our `forEach` loop called `books`. The `viewBooks` method is assigning the list of books retrieved from the database to that attribute. Now, the browser will have access to the data when it tries to render it.

We're going to come back to this class a few times to improve it. We want to be able to add, edit, and delete books, so we'll need to add routes to recognize and process those actions. And we're going to get rid of the plaintext configuration and credentials in our constructor. That's very bad practice, so we'll clean that up, too.

### Configurations

To allow our servlet to recognize and respond to web requests, we need to do some configuration. All of our configuration is going to go in a file called `web.xml`. Right-click the project and click `New > File`. Put this file in the `WebContent/WEB-INF` folder.

![Configurations](.gitbook/assets/web-configs.png)

We're going to add just what we need at the moment, but we will be back to add more. This is another one of those times where you can copy and paste. This stuff needs to be exactly right.

```markup
<?xml version="1.0" encoding="UTF-8"?>

<web-app
  xmlns="http://xmlns.jcp.org/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
  version="4.0"
>
  <display-name>UCVTS Library</display-name>
  
  <context-param>
    <param-name>JDBC-URL</param-name>
    <param-value>jdbc:mysql://localhost:3306/library?serverTimezone=EST</param-value>
  </context-param>
  <context-param>
    <param-name>JDBC-USERNAME</param-name>
    <param-value>root</param-value>
  </context-param>
  <context-param>
    <param-name>JDBC-PASSWORD</param-name>
    <param-value>rootpwd!</param-value>
  </context-param>
  
  <servlet>
    <servlet-name>Controller</servlet-name>
    <servlet-class>application.Controller</servlet-class>
  </servlet>
  
  <servlet-mapping>
    <servlet-name>Controller</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app>
```

You'll see references to our MySQL username and password, so make sure you enter the information you setup while installing MySQL. The username and password values are specific to my instance.

### Revisions

Now that we are storing our JDBC settings in `web.xml`, we can remove the plaintext references to the `url`, `username`, and `password`. Take a look at the `init` method in `Controller.java`.

The only changes we're making are in the `init` method.

![Revised Source Code for Servlet Class](.gitbook/assets/servlet-code-revised.png)

Much better! Our servlet is just a little more secure. While we're at it, we don't need `Main.java` anymore. You can go ahead and delete it and the `demo` package.

## Deployment Assembly

One more thing to do before we test our code. We need to make sure Eclipse knows to include our Maven dependencies in the deployment. Right-click the project and click `Properties`, then select `Deployment Assembly`.

![Deployment Setup](.gitbook/assets/deployment-1.png)

See? Our Maven dependencies are nowhere to be found. Let's change that. Click the `Add` button, then select `Java Build Path Entries`.

![Deployment Setup](.gitbook/assets/deployment-2.png)

Now, click `Next >` and select `Maven Dependencies`.

![Deployment Setup](.gitbook/assets/deployment-3.png)

Click `Finish`, and you should now see a reference to the `Maven Dependencies` folder. Click `Apply and Close`.

![Deployment Setp](.gitbook/assets/deployment-4.png)

### Testing the Application

Starting Tomcat is easy. Open the `Servers` tab. You should see `Tomcat v9.0 Server at localhost` \(or whatever you named your server\). Right-click it and select `Add and Remove...`.

![Tomcat Configuration](.gitbook/assets/tomcat-add-1.png)

Our project is available, but not configured. Select ucvts-library and click `Add >`.

![Tomcat Configuration](.gitbook/assets/tomcat-add-2%20%281%29.png)

Click Finish. Next, right-click the server again and click `Start`. If you get an error saying that Tomcat is already in use, it's probably because you never shut it down when testing your installation. Go back to the installation directory and run the `shutdown.bat` or `shutdown.sh` script.

![Startup Error](.gitbook/assets/tomcat-error.png)

In your browser, navigate to `http://localhost:8080/ucvts-library/`. If you did everything right, you should see our books rendering on the page.

![Application](.gitbook/assets/working-app.png)

Things are finally starting to come together! Next, we'll start adding feature to allow users to add, modify, and delete books from the library's collection.

## Adding Functionality

Now that our application renders some basic information, let's start working on adding the desired functionality. First, let's add a few things to `inventory.jsp`.

In the first `div` underneath `Inventory Management`, let's replace the existing `h2` and `a` tag with some basic navigation to view and add books. We'll also add one more column \(and the associated data\) to our `table`, so that a user, such as a librarian, can rent, return, or edit books.

![Revised Markup for Inventory JSP](.gitbook/assets/inventory-jsp-3.png)

Refresh the application and you should see the changes we just made.

![Application](.gitbook/assets/revised-app.png)

Don't worry about any discolorations in your links. We'll be adding styling later.

### Renting and Returning Books

Let's start with the `RENT` and `RETURN` features. When a user clicks one of these, the number of available books should either decrease or increase. We'll begin by modifying the `Book` class.

First, remove the `setAvailable` method. Since users are going to be renting and returning books, it makes more sense to have `rentMe` and `returnMe` methods. These will be in charge of updating the number of available copies, as well as verifying that this is even possible. We can't rent a book if all of our copies are already checked out!

Here's the new-and-improved `Book` class. The new methods are at the bottom.

![Revised Source Code for Book Class](.gitbook/assets/book-code-revised.png)

Now, on to our servlet. We'll update the `switch` statement in our `doGet` method. And, since we're calling a new `updateBook` method from within that `switch` statement, we'll write that method, too.

![Revised Source Code for Servlet Class](.gitbook/assets/servlet-code-revised-again.png)

Perfect. Now, we can click those `RENT` and `RETURN` links and the number of available copies will change accordingly.

### Adding, Editing, and Deleting Books

Now that we can rent and return a book, we need a way to add, edit, and delete books. We're going to use a single JSP file called `bookform.jsp` to represent these actions. Right-click the `WebContent` folder and click `New > JSP File`.

![BookForm JSP File](.gitbook/assets/bookform-jsp-1.png)

In our newly created JSP file, we're going to construct a dual purpose form: adding new books, and editing or deleting existing ones.

![BookForm JSP File](.gitbook/assets/bookform-jsp-2.png)

We display one of two forms, depending on whether there is a valid instance of the `Book` class. In the `Controller` class, again, we'll be updating our `switch` statement. A portion of the class is cut off, but we're focused only on the `switch` statement in `doGet` and `showEditForm`. Nothing else changed.

![Revised Source Code for Servlet Class](.gitbook/assets/servlet-code-revised-more.png)

We're intentionally falling through in our `switch` statement here. We want the `showEditForm` method to run for both `/add` and `/edit` paths. We still need to implement the form functionality, but we do have two successfully rendering forms. The form for adding new books to the library.

![Add Form](.gitbook/assets/add-form-1.png)

And another for editing \(or deleting\) existing books.

![Edit and Delete Form](.gitbook/assets/edit-form-1.png)

Let's get the editing form up and running. We've got two jobs: editing and deleting. And even though we initially left out setters for `title`, `author`, and `available`, we're going to let users edit those values. Maybe someone typed them in wrong when adding a book. It happens. And if we change total copies, we'll need to change the number of copies available, too.

Add setters for those three fields in the `Book` class.

![Revised Source Code for Book Class](.gitbook/assets/book-code-revised-again.png)

Let's make our error-handling a little easier, too. We don't want to check every time if the user entered a number. We're going to force their hand with a dropdown menu. Replace the `input` tag in `bookform.jsp` for `# of Copies` with a `select` tag.

![Revised Markup for BookForm JSP](.gitbook/assets/bookform-jsp-3.png)

And last, but not least, we'll modify our `Controller`. Let's revise the `updateBook` method, and add a `deleteBook` method.

![Revised Source Code for Servlet Class](.gitbook/assets/servlet-code-revised-all.png)

Now we can rent, return, edit, and delete books! Let's get started on adding books. We'll need to make yet another change to our Controller class. You guessed it! A change to the `switch` statement in `doGet`, and a new method called `insertBook`.

![Revised Source Code for Servlet Class](.gitbook/assets/servlet-code-revised-final.png)

## Styling the Application

Now that everything is functional, let's take a look at the aesthetics.

### Inventory

We'll start with our `invetory.jsp` page. We're going to tweak the JSP in preparation for adding styles.

![Revised Markup for Inventory JSP](.gitbook/assets/inventory-jsp-4.png)

Now, we'll add some CSS. First, right-click the `WebContent` folder and click `New > Folder`. Call the folder `css`.

![New Folder](.gitbook/assets/css-folder.png)

Then, right-click the newly created `css` folder and click `New > File`. Call the file `styles.css`.

![New Stylesheet](.gitbook/assets/css-file.png)

And, last but not least, add your styles. I've included two screenshots of the same file, simply because it was too large for a single image.

![Styles \(lines 1-51\)](.gitbook/assets/styles-1.png)

![Styles \(lines 52-93\)](.gitbook/assets/styles-2.png)

So far, so good. Our `inventory.jsp` page is all styled. Let's startup our server and have a look.

![Inventory JSP with Styles](.gitbook/assets/styled-inventory.png)

### Form

Moving on to our `bookform.jsp` page, which serves as our form for adding, editing, and deleting books. Let's start with a few tweaks to the JSP.

![Revised Markup for BookForm JSP](.gitbook/assets/bookform-jsp-4.png)

We need to add a few more things to our `styles.css` file, too \(again, split between two screenshots\).

![Styles \(lines 1-66\)](.gitbook/assets/styles-3.png)

![Styles \(lines 66-129\)](.gitbook/assets/styles-4.png)

And now for the final versions of our `bookform.jsp` page!

![Add Form with Styles](.gitbook/assets/add-form-2.png)

![Edit and Delete Form with Styles](.gitbook/assets/edit-form-2.png)

Congratulations! Your very first Java EE application! Feel free to use this application as a template for future projects using this technology stack.

## Extra Credit

As a librarian, it might get a bit overwhelming sorting through all these books. It would be nice to be able to sort by title, author, the number of copies, or the number of copies available.

Implement a sort feature on each of the four data columns. Sorting should work in both directions \(i.e., ascending and descending\), and you'll be critiqued both on functionality, as well as how seamlessly you integrate this feature into the UI.

## Deliverables

1. Submit your repository URL.
2. Submit a video demo for the tutorial + optional extra credit \(between 3 and 5 minutes\).

Follow the tutorial and implement a working UCVTS Library application with a database and web server. It should match mine in every way. From there, should you so choose, your code will diverge from that of the tutorial as you implement the optional extra credit.

Your video demo must show the working tutorial, including the ability to add, edit, delete, rent, and return books. If you elect to implement the extra credit, it must also highlight the ability to sort each of the four data columns ascending and descending.

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, January 10, 2021.

