# PHP Login/Registration Project for Sustiere Lifestyle Blog

## Contents

### Project overview

### Requirements

### Languages

### Database and Table Connection

### Existing User Tests

### Project Structure

### Functionality

## Project overview

This project provides a functional signup/login system wherein users can register for an account and use login details to access the account. Data used to create an account is stored in a MySQL database and queries are used to retrieve and compare data to enable login to acccounts in the future.

## Requirements

- PHP
- Apache Server
- MySQL

## Languages

- PHP-8.1
- HTML5
- CSS3

## Database and table connection

Host- "localhost"
User- "root"
Password- ""
table "signup"

Alternatively to connect to database connection.php can be utilised using `include` within file.

**Connection only for the functionality. Do not edit.**

## Existing user sample for testing purposes

username: Misspiggy
password: 1Lovekermit!

## Project structure

**Registration Page:**

- registrationform.php
- signup.php

**Login Page:**

- loginform.php
- login.php

**Homepage:**

- homepage.php

**Logout Handler**

- logout.php

  **Database Connection/Table Creation:**

- create_table.php
- connection.php

**Error Handling**

- messages.php

**CSS:**

-style.css
-loginform.css

## Functionality

**Signup**

The signup.php file contains a PHP script that handles user registration. Database connection file (conn.php) is included to establish connection to the database and table for data to be input. The script retrieves the values input by the user on the registrationform.php file and then sequencial script conducts data validation. If all validation tests are true, using SQL the query **"INSERT INTO users(username, email, pass) VALUES ('$name', '$email', '$pass')"** data is inserted into the user table contained on the database and user is directed to the login page using `location: example_destination.php` If a validation check fails page redirects to registration form and an indicative error message stored in an array of error messages is displayed to the user who can then easily identify error, fix and resubmit.

Validation checks are as follows:

-Any empty fields using empty() function.

if (empty($data['uName']) || 
empty($data['email']) ||
empty($data['pass']) ||
empty($data['confirm_pass']))

- Regular expression for required username format (between 5-20 characters and contain no spaces)

/^[\w\d\_][^\s]{5,20}$/

- Regular expression for required password format (between 6-20 characters at least 1 capital letter, 1 special character and 1 number)

/^(?=._[A-Z])(?=._[0-9])(?=.\*[\W]).{6,20}$/

- Regular expression for email to ensure email capture is in the correct format

/^([a-zA-Z0-9\.-])+@([a-zA-Z0-9]+).([a-z]{2,10}).([a-z]{2,8})?$/

- Check to ensure passwords are matching

$data['pass'] !== $data['confirm_pass']

Validation is also set to check if a user alrady exists by retrieveing and comparing data from existing table using **"SELECT \* FROM `users` WHERE email = '$email'"**

**Login**

The login.php file contains a PHP script that handles existing users. Database connection file (conn.php) is included to establish connection to the database and table for data to be retrieved and compared. The script dynamically retrieves the username and password values input by the user from the loginform.php file using variables and is then used in an SQL SELECT query to search for existing users on the table where username and password are equal to existing rows. **"SELECT \* FROM `users` WHERE username = '$name' & pass = '$pass'"**. This query is executed with the mysqli_query() function which is then stored in a variable. This is then passed to mysqli_fetch_assoc() function to retrieve the result. If the result turns true (contains retrieved data)the file redirects to the homepage using the header function with the location paramater set to homepage.php. However, if the result is false an error message lets the user know the system hasn't been able to find the user or informs the user the password has been entered incorrectly.

The empty() function is utilised to ensure that all fields are filled in. Subsequently if a field is vacant an error message is displayed to the user to ensure all fields are complete before submitting.

**Homepage welcome and logout button**

Upon successeful login the homepage will display a welcome message with a dynamic value that has been caputered on the login page using the username variable. It will directly welcome the user to their homepage which is achieved by the session storing the variable value from the login form and then echoing that value back on the homepage.

Finally the logout button posts a request that uses the session_unset() and session_destroy() functions which will unset session variables and then destros .current data thats associated with the current session consequently logging the user out and redirecting them back to the login page.

**Messages**
messages.php starts with Session_start() function to allow access to access the message variable.
The messages.php file will check if the messages array is empty. if it is not empty due to the failure of a validation check it will retrieve the suitable error message to communicative to the user by embedding into the current displayed file using the require_once keyword. If all validation is true the unset() function is used to clear the variable for future use.

**Connection**

The conn.php file creates the connection to the database using mysqli_connect() function with variables containing host name, username, database name and password passed through the paramaeters. There is communication to the developer as an asterisk in the instance the connection has been successful. If connection has failed error message is passed to the messages array and is communicated to the developer.
