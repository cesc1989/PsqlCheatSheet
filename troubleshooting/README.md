# Troubleshooting

This section covers solutions for some things that didn't work well when I tried them.

## invalid byte sequence for encoding “UTF8”

When you backup a database with `pg_dump` command, as far as I know, you cannot<sup>[[1]][sto] [[2]][dba]</sup> restore that database from that file using `pg_restore`. The reason behind this is that the output file produced by `pg_dump` is not readable by `pg_restore`.

You should restore a backup with `psql` command. However, sometimes you would stomp with error:

    $ ERROR:  invalid byte sequence for encoding "UTF8":

I'm not really sure why this happens but this is easily solvable. You need to fix the encoding of the file using a tool called `iconv` as follows:

    $ iconv -t utf-8 /path/to/file > /path/to/fixed_dump

> [Read more about `iconv`](https://linux.die.net/man/1/iconv)

Now, you can use `fixed_dump` to restore your database using `psql` command:

    $ psql [db_name] --host [host_name] --username [username] < /path/to/fixed_dump


[sto]: http://stackoverflow.com/a/4867690/1407371 "Stack Overflow"
[dba]: http://dba.stackexchange.com/a/4781/69085 "DBA exchange"
