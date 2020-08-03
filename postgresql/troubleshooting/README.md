# Troubleshooting

This section covers solutions for some things that didn't work well when I tried them.

## invalid byte sequence for encoding “UTF8”

When you backup a database with `pg_dump` command, as far as I know, you [cannot](http://stackoverflow.com/a/4867690/1407371) [restore](http://dba.stackexchange.com/a/4781/69085) that database from that file using `pg_restore`. The reason behind this is that the output file produced by `pg_dump` is not readable by `pg_restore`.

You should restore a backup with `psql` command. However, sometimes you would stomp with error:

    $ ERROR:  invalid byte sequence for encoding "UTF8":

I'm not really sure why this happens but this is easily solvable. You need to fix the encoding of the file using a tool called `iconv` as follows:

    $ iconv -t utf-8 /path/to/file > /path/to/fixed_dump

> [Read more about `iconv`](https://linux.die.net/man/1/iconv)

Now, you can use `fixed_dump` to restore your database using `psql` command:

    $ psql [db_name] --host [host_name] --username [username] < /path/to/fixed_dump

## dyld: Library not loaded

Found this error after installing PostgreSQL in MacOS.

```
dyld: Library not loaded: /usr/local/opt/openssl/lib/libssl.1.0.0.dylib
 Referenced from: /usr/local/Cellar/postgresql/11.4/lib/libpq.5.11.dylib
 Reason: image not found
[1]  7064 abort   psql
```

What worked in that specific situation was to reinstall Postgres but also run some Homebrew commands to make sure everything was alright.

```
$ brew uninstall --force postgresql
$ rm -rf /usr/local/var/postgres
$ brew doctor
$ brew update # If there are errors, run any command Brew tells you to
$ brew install postgresql
$ brew services start postgresql
$ createdb $(whoami)
```

## PG::ConnectionBad or could not connect to server

This error

```
psql: error: could not connect to server: could not connect to server: No such file or directory
	Is the server running locally and accepting
	connections on Unix domain socket "/tmp/.s.PGSQL.5432"?
```

If `brew services restart postgresql` doesn't work try `rm /usr/local/var/postgres/postmaster.pid`.

Seen at [Stack Overflow](https://stackoverflow.com/a/18832331/1407371).

If above commands don't work, run `postgres -D /usr/local/var/postgres` to get an ouput of what's going on.

Example:

```
2020-08-03 16:08:47.900 -05 [76016] FATAL:  database files are incompatible with server
2020-08-03 16:08:47.900 -05 [76016] DETAIL:  The data directory was initialized by PostgreSQL version 11, which is not compatible with this version 12.3.
```

The second error message can be solved with `brew postgresql-upgrade-database`.

Seen at [Stack Overflow](https://stackoverflow.com/a/48409221/1407371)
