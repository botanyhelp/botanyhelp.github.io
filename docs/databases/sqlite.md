## Sqlite

Using SQLite by Jay A. Kreibich is the best SQLite book.  The most under-appreciated way to learn about sqlite is in sqlite itself by typing **.help** at the sqlite command line.  

I will do that for you right here:

```
$ sqlite3 
SQLite version 3.6.20
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite> .help
.backup ?DB? FILE      Backup DB (default "main") to FILE
.bail ON|OFF           Stop after hitting an error.  Default OFF
.databases             List names and files of attached databases
.dump ?TABLE? ...      Dump the database in an SQL text format
                         If TABLE specified, only dump tables matching
                         LIKE pattern TABLE.
.echo ON|OFF           Turn command echo on or off
.exit                  Exit this program
.explain ON|OFF        Turn output mode suitable for EXPLAIN on or off.
.genfkey ?OPTIONS?     Options are:
                         --no-drop: Do not drop old fkey triggers.
                         --ignore-errors: Ignore tables with fkey errors
                         --exec: Execute generated SQL immediately
                       See file tool/genfkey.README in the source 
                       distribution for further information.
.header(s) ON|OFF      Turn display of headers on or off
.help                  Show this message
.import FILE TABLE     Import data from FILE into TABLE
.indices ?TABLE?       Show names of all indices
                         If TABLE specified, only show indices for tables
                         matching LIKE pattern TABLE.
.load FILE ?ENTRY?     Load an extension library
.mode MODE ?TABLE?     Set output mode where MODE is one of:
                         csv      Comma-separated values
                         column   Left-aligned columns.  (See .width)
                         html     HTML <table> code
                         insert   SQL insert statements for TABLE
                         line     One value per line
                         list     Values delimited by .separator string
                         tabs     Tab-separated values
                         tcl      TCL list elements
.nullvalue STRING      Print STRING in place of NULL values
.output FILENAME       Send output to FILENAME
.output stdout         Send output to the screen
.prompt MAIN CONTINUE  Replace the standard prompts
.quit                  Exit this program
.read FILENAME         Execute SQL in FILENAME
.restore ?DB? FILE     Restore content of DB (default "main") from FILE
.schema ?TABLE?        Show the CREATE statements
                         If TABLE specified, only show tables matching
                         LIKE pattern TABLE.
.separator STRING      Change separator used by output mode and .import
.show                  Show the current values for various settings
.tables ?TABLE?        List names of tables
                         If TABLE specified, only list tables matching
                         LIKE pattern TABLE.
.timeout MS            Try opening locked tables for MS milliseconds
.width NUM NUM ...     Set column widths for "column" mode
.timer ON|OFF          Turn the CPU timer measurement on or off
sqlite>
```

You are welcome.

The [Fighterjets](/software/android.md#Fighterjets) android application contains an sqlite3 database that has all of the fighter jet data inside of it.  That database was created with this sqlite creation SQL:

```
CREATE TABLE fighter (name text default null, country text default null, firstyear text default null, number text default null, status text default null, info text default null);

.read fighter.sql

CREATE INDEX idxname  ON  fighter(name);
CREATE INDEX idxcountry  ON  fighter(country);
CREATE INDEX idxfirstyear  ON  fighter(firstyear);
CREATE INDEX idxnumber  ON  fighter(number);
CREATE INDEX idxstatus  ON  fighter(status);
CREATE INDEX idxinfo ON  fighter(info);
```

There is one table, named fighter, with 6 columns.  The sqlite command **.read** then consumes a bunch of **INSERT** SQL statements that fill the fighter table.  Then we create an index for every column.  Because this database is read only, those indexes will only speed things up by making the **SELECT** queries much faster. 

A small INSERT statement (and a sad one) found in fighter.sql is this one:

```
INSERT INTO fighter (name,country,firstyear,number,status,info) VALUES ('Albree Pigeon-Fraser Pursuit', 'United States', '1917', '3', 'Abandoned','');
```
