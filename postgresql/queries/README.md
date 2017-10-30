# Queries

This section covers queries for setting up users in a new PostgreSQL database.

## Create New User

You need to access the psql command-line in order to administrate users

Start by login in as `postgres` user

    $ sudo su postgres

then proceed to `psql` console

    postgres:$ psql

and you're now logged in and ready to start

    psql (9.3.18)
    Type "help" for help.

    postgres=#

>Note: You have the shortcuts `sudo -u postgres psql` and `sudo su postgres -c psql`

### Create User & Role with Superuser Privileges

    postgres=# CREATE ROLE [username] SUPERUSER;

### Enable Login for this User

    postgres=# ALTER ROLE [username] WITH LOGIN;

### Change Password

    postgres=# ALTER USER "username" WITH PASSWORD 'password';

> Note: Found in SOF: http://stackoverflow.com/a/23934693

### Shortcuts

Create user & role with password:

    postgres=# CREATE ROLE [username] WITH LOGIN ENCRYPTED PASSWORD 'password';

Create user & role with specific privileges:

    postgres=# CREATE ROLE [username] WITH LOGIN ENCRYPTED PASSWORD 'password' CREATEDB CREATEROLE REPLICATION SUPERUSER;

## Getting Help

In the psql command-line type `\h` for SQL available commands and `\?` for a list of psql commands.
