# psqlCommands

## Connect to PostgreSQL database

The following command connects to a database under a specific user. After pressing Enter PostgreSQL will ask for the password of the user.

```bash
psql -d database -U  user -W
```

For example, to connect to dvdrental database under postgres user, you use the following command:

```bash
psql -d dvdrental -U postgres -W
Password for user postgres:
dvdrental=#
```

If you want to connect to a database that resides on another host, you add the -h option as follows:

```bash
psql -h host -d database -U user -W
```

In case you want to use SSL mode for the connection, just specify it in the command as the following command:

```bash
psql -U user -h host "dbname=db sslmode=require"
```

## Switch connection to a new database

Once you are connected to a database, you can switch the connection to a new database under a user specified by user. The previous connection will be closed. If you omit the user parameter, the current user is assumed.

```bash
\c dbname username
```

The following command connects to dvdrental database under postgres user:

```bash
postgres=# \c dvdrental
You are now connected to database "dvdrental" as user "postgres".
dvdrental=#
```

## List available databases

To list all databases in the current PostgreSQL database server, you use \l command:

```bash
\l
```

## List available tables

To list all tables in the current database, you use \dt command:

```bash
\dt
```

Note that this command shows only table in the current connected database.

## Describe a table

To describe a table such as a column, type, modifiers of columns, etc., you use the following command:

```bash
\d table_name
```

## List available schema

To list all schema of the currently connected database, you use the \dn command.

```bash
\dn
```

## List available functions

To list available functions in the current database, you use the \df command.

```bash
\df
```

## List available views

To list available views in the current database, you use the \dv command.

```bash
\dv
```

## List users and their roles

To list all users and their assign roles, you use \du command:

```bash
\du
```

## Execute the previous command

To retrieve the current version of PostgreSQL server, you use the version() function as follows:

```bash
SELECT version();
```

Now, you want to save time typing the previous command again, you can use \g command to execute the previous command:

```bash
\g
```

psql executes the previous command again, which is the SELECT statement,.

## Command history

To display command history, you use the \s command.

```bash
\s
```

If you want to save the command history to a file, you need to specify the file name followed the \s command as follows:

```bash
\s filename
```

## Execute psql commands from a file

In case you want to execute psql commands from a file, you use \i command as follows:

```bash
\i filename
```

## Get help on psql commands

To know all available psql commands, you use the \? command.

```bash
\?
```

To get help on specific PostgreSQL statement, you use the \h command.

For example, if you want to know detailed information on ALTER TABLE statement, you use the following command:

```bash
\h ALTER TABLE
```

## Turn on query execution time

To turn on query execution time, you use the \timing command.

```bash
dvdrental=# \timing
Timing is on.
dvdrental=# select count(*) from film;
 count
-------
  1000
(1 row)

Time: 1.495 ms
dvdrental=#
```

### You use the same command \timing to turn it off

```bash
dvdrental=# \timing
Timing is off.
dvdrental=#
```

## Edit command in your own editor

It is very handy if you can type the command in your favorite editor. To do this in psql, you \e command. After issuing the command, psql will open the text editor defined by your EDITOR environment variable and place the most recent command that you entered in psql into the editor.

```bash
psql commands
```

After you type the command in the editor, save it, and close the editor, psql will execute the command and return the result.

```bash
psql command example
```

It is more useful when you edit a function in the editor.

```bash
\ef [function name]
psql commadn ef edit function
```

## Switch output options

psql supports some types of output format and allows you to customize how the output is formatted on fly.

```bash
 \a command switches from aligned to non-aligned column output.
 \H command formats the output to HTML format.
```

## Quit psql

To quit psql, you use \q command and press enter to exit psql.

```bash
\q
```

In this tutorial, we have shown you how to use psql commands to perform various commonly used tasks.

[Source](http://www.plsqltutorial.com/)