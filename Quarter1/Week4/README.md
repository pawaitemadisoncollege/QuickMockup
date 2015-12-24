[<<Main Navigation](https://github.com/bciancio/QuickMockup/blob/master/README.md#quickmockup) [<<QuarterOne](https://github.com/bciancio/QuickMockup/tree/master/Quarter1)

# Week 4

### When you arrive
1. Sign in on the paper sign in sheet.

## Week 3 Review
1. Code walkthrough in pairs - Find and Replace Unit Tests
1. Code walkthrough in pairs - Form-based Authentication Web App
1. Individual Project Overviews

## Logging
1. Using Log4J, add logging to the Find and Replace program.
    1. Add Log4J.jar to your project.
    1. Create and configure log4j.properties.
    1. Add log statements to your program.
    1. Practice with various logging levels. INFO, DEBUG, etc.

## Security - A More Practical Set-up

In order to do more realistic security checking in our applications, we should store userids, roles and passwords outside of the server. For this exercise, we will put our user and role information in a database.

### MySQL Installation 

1. Install MySQL (Community Server edition) if you do not already have it installed
    1. Download the installation file from [here](http://dev.mysql.com/downloads/mysql/).
    1. Run the installation.
    1. Start MySQL Server
        * Windows: Program Files >> MySQL
        * Mac: System Preferences >> MySQL 
    1. At the command line, navigate to the installation directory
        * Windows: This is automatic when you open the MySQL Command Line Client
        * Mac: 
            * usr/local/mysql
            * consider adding aliases to simplify this access
                * alias mysql=/usr/local/mysql/bin/mysql
                * alias mysqladmin=/usr/local/mysql/bin/mysqladmin

### Create the Database and Tables

1.Create a new database
        
        mysql> CREATE DATABASE SAMPLE;
        Query OK, 1 row affected (0.00 sec)
    
1. Select the database you just created

        mysql> use sample
        Database changed
        mysql> 
    
1. Create a user table

        create table users (
        user_name         varchar(15) not null primary key,
        user_pass         varchar(15) not null
        );
    
1. Create a user_roles table

        create table user_roles (
        user_name         varchar(15) not null,
        role_name         varchar(15) not null,
        primary key (user_name, role_name)
        );

1. Create a user so that Tomcat can access the database you just created.

        mysql> CREATE USER 'tomcat'@'localhost' IDENTIFIED BY 'tomcat';
        Query OK, 0 rows affected (0.00 sec)

1. Give the tomcat user privileges to read.

        mysql> GRANT SELECT ON sample.* TO 'tomcat'@'localhost';

1. Create some users:

        mysql> insert into users values ('admin', 'admin');
        Query OK, 1 row affected (0.01 sec)

1. Confirm the users were added: 

        mysql> select * from users;

1. Add some roles: 

        mysql> insert into user_roles values ('admin', 'administrator');
        Query OK, 1 row affected (0.01 sec)

1. Confirm the roles were added 

        mysql> select * from user_roles;

### Set up Tomcat to use JDBCRealm

Refer to the JDBCRealm portion of this [page](https://tomcat.apache.org/tomcat-8.0-doc/realm-howto.html) to configure tomcat to use the tables you just set up.

### Test using your form-based authentication application. 


        
