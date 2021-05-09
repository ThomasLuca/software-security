# SQL Injections

On a server, long-lived data (login credentials/ content) lives in a database. These databases are build and maintained in a language like SQL.

## Server-side data

* Typically wants ACID translations
  * Atomicity: transactions should complete entirely or not at all.
  * Consistency: Data in database is always in valid state.
  * Isolation: Result from transactions aren't visible until completed.
  * Durability: Once a transactions is committed, its effects persist despite stuff like power failures.

* To achieve ACID we use __Database Management Systems__ (DBMes)

## SQL (Standard Query Language)

Data is stored in tables. Server side code will interact with the database using SQL. This server side code is often written in a language like (PHP/ nodejs).

## SQL injection

User input that needs to be stored in a database is send to the server using queries. If the user provides SQL code inside the input field, than there is a possibility that the query will interpret the user input as valid SQL code. This results in a SQL injections.

eg:
injection code in username field

* username: `frank' OR 1=1); DROP TABLE Users; --`
* password: `whocares`

php:

```php
$result = mysql_query("select * from Users where(
    name='$user' and password='pass');");
                    |
                    v
$result = mysql_query("select * from Users where(
    name='frank' OR 1=1);
    DROP TABLE Users; --
    and password='whocares');");
```

How to defend? -> Sanitize database input.
