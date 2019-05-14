# Basic Stuff

## Install PostgreSQL in macOS

Best way is using [Homebrew](https://brew.sh/)

```bash
$ brew install postgresql
```

## Uninstall PostgreSQL from macOS

Also doable with Brew:

```bash
$ brew uninstall --force postgresql
```

Then make sure everything is gone, if needed:

```bash
$ rm -rf /usr/local/var/postgres
```

## Create system user database to login to PSQL

In order to use the interactive postgres console we need to have a user with password, impersonate postgres user(in the form of `sudo su postgres -c psql`).

To create our system user database we issue the next command:

```bash
$ createdb $(whoami)
```

Now you can do:

```bash
$ psql
```

And login normally.

Can also be deleted with:

```bash
$ dropdb $(whoami)
```