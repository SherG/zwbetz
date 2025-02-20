---
title: "Connect to an Oracle Database and Run a Query From a Bash Script"
summary: "Get Oracle and Bash to play nice."
date: 2019-06-07T13:09:06-05:00
toc: true
---

## Prerequisites 

- `sqlplus` (SQL*Plus) version 12.2.x or higher is installed and on your `PATH`. See install steps for [Mac]({{< relref "install-sqlplus-on-a-mac" >}}) and [Linux]({{< relref "install-sqlplus-on-linux" >}})
- The following files are in the same directory

## Files 

A `query.sql` file:

```sql
-- this file must end in a new line
SELECT 'foo'
FROM dual
WHERE 1 = 1
UNION ALL
SELECT 'bar'
FROM dual
WHERE 2 = 2;
```

An `.env` file:

```bash
ORACLE_HOST='localhost'
ORACLE_PORT='1521'
ORACLE_DATABASE='some_database'
ORACLE_USERNAME='some_user'
ORACLE_PASSWORD='some_password'
```

A `script.sh` file:

```bash
#!/usr/bin/env bash

# Load database connection info
set -o allexport
source .env
set +o allexport

# Read sql query into a variable
sql="$(<"query.sql")"

# If sqlplus is not available, then exit
if ! command -v sqlplus > /dev/null; then 
  echo "This script requires sqlplus to be installed and on your PATH ..."
  exit 1 
fi 

# Connect to the database, run the query, then disconnect
echo -e "SET PAGESIZE 0\n SET FEEDBACK OFF\n ${sql}" | \
sqlplus -S -L ${ORACLE_USERNAME}/${ORACLE_PASSWORD}@${ORACLE_HOST}:${ORACLE_PORT}/${ORACLE_DATABASE}
```

## Usage

Make it executable:

```
$ chmod 755 script.sh
```

Print results to stdout:

```
$ ./script.sh
foo
bar
```

Write results to file:

```
$ ./script.sh > results.txt
```

## Notes

- The `SET PAGESIZE 0` option suppresses all headings, page breaks, titles, the initial blank line, and other formatting information
- The `SET FEEDBACK OFF` option suppresses the number of records returned by a script
- The `-S` option sets silent mode which suppresses the display of the SQL*Plus banner, prompts, and echoing of commands
- The `-L` option attempts to log on just once, instead of reprompting on error

## Related

- [Connect to a Postgresql Database and Run a Query From a Bash Script]({{< relref "connect-to-a-postgresql-database-and-run-a-query-from-a-bash-script" >}})
- [Set Environment Variables in Your Bash Shell From a .env File (Version 2)]({{< relref "set-environment-variables-in-your-bash-shell-from-a-env-file-version-2/index.md" >}})
