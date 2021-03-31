# SQL injection countermeasures

## The underlying issue

A query string is a combination of both code and data (similar to buffer overflow).

## Prevention = Input Validation

The input must be validated before it is trusted.

How to make data trustworthy:

* Check if it has the expected form
* Sanitize it by modifying it or using it in a certain way that the result is correctly formed by construction.

### Blacklisting (Sanitization)

* Delete characters that you don't want. eg: `', ;, --`.

* Downside: `"Peter O'Connor"`, sometimes these characters are needed.

### Escaping (Sanitization)

Replace problematic characters with safe ones:

* ' -> \\'
* ; -> \\;
* \- -> \\-
* \ -> \\\

Or use libraries that do just that.

__Downside__:

* Sometimes you also want the replaced characters in the SQL.
* This approach can also be not enough

### Whitelisting (Checking)

* Check that user input is known to be safe
* Rationale: given an invalid input, it's safer to reject than to fix

__Downside__:

* Hard to decide what to whitelist.

### Prepared Statements (Sanitization)

This is the preferred method.

* Treat user data according to its type

eg:

```php
$result = mysql_query("select * from Users where(
    name='$user' and password='pass');");

                    |
                    v

$db = mysql_query("localhost", "user", "pass", "DB");
$statement = $db->prepare("select * from Users where(name=? and password=?);");

$statement->bind_params("ss", $user, $pass); # Bind vars are typed as string
$statement->execute();
```

## Mitigate

It's best practice to mitigate the effect a SQL injection could possible have.

* Limit privileges (limit commands and/or tables a user can access)
* Encrypt sensitive data stored in the database
