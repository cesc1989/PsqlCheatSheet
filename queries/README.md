# Queries

This section covers queries for setting up users in a new postgresql database.

## Create New User

First, you need to access psql console as `postgres` user

    $ sudo su - postgres

then proceed to `psql` console.

>Note: You have the shortcut `sudo -u postgres psql`

### Create User & Role with Superuser Privileges

    db_name=# CREATE ROLE [username] SUPERUSER;

### Enable Login for this User

    db_name=# ALTER ROLE [username] WITH LOGIN;

#### Change Password

    db_name=# ALTER USER "username" WITH PASSWORD 'password';

> Note: Found in SOF: http://stackoverflow.com/a/23934693

### Shortcuts

Create user & role with password:

    db_name=# CREATE ROLE [username] WITH LOGIN ENCRYPTED PASSWORD 'password';

Create user & role with specific privileges:

    db_name=# CREATE ROLE [username] WITH LOGIN ENCRYPTED PASSWORD 'password' CREATEDB CREATEROLE REPLICATION SUPERUSER;
