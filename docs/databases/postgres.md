## Postgres

Learning and running PostgreSQL is rather more painful than MySQL.  Opportunities to run PostgreSQL seem to be increasing.  Some of those opportunities are the **must use PostgreSQL** kind.  For exampple, setting up and running [Openclinica](https://docs.openclinica.com/3.1/technical-documents) is done with Postgres.  The (free) persistent database running at [Heroku](/linux/heroku.md) is Postgres and so you'll need to run one yourself when developing a database backed application that is going to run on Heroku.  The best books for learning PostgreSQL are:

* PostgreSQL: Up and Running, 2nd Edition by Regina O. Obe, Leo S. Hsu
* Practical PostgreSQL by Joshua D. Drake, John C. Worsley

Practical PostgreSQL is old but still useful as a reference. 

Openclinica, mentioned above, is a very powerful open source clinical research application.  Administrators with linux and LAMP experience will find its documentation to be excellent.  Setting up OpenClinica using the online documentation is not too difficult and will step through the operations of setting up an enterprise Postgres application server.  This is a good way to learn about Postgres and can be done in a few days.  

### Simple postgres database for Rails application

Here we describe how to setup Postgres on CentOS so that it can support the [Heroku](/linux/heroku.md) application when running locally on linux.  You will want to set your RoR and Postgres application on a local linux box before trying to send it off to run on Heroku.

Ruby on Rails takes care of most of the Postgres administration for you because you describe your database in the application.  For the [Heroku](/linux/heroku.md) application mentioned above, the [schema.db](https://github.com/botanyhelp/Herokucarriers/blob/master/db/schema.rb) file will have the table setup the way the application expects.  The ruby also tells the database name in [database.yml](https://github.com/botanyhelp/Herokucarriers/blob/master/config/database.yml).  Start by installing postgres, perhaps like this on CentOS6:

```
yum --enablerepo=pgdg93 install postgresql93-server postgresql93-contrib
service postgresql-9.3 initdb
chkconfig postgresql-9.3 on
service postgresql-9.3 start
```

Then read [wiki.postgresql.org/wiki/First_steps](http://wiki.postgresql.org/wiki/First_steps) and do it.  

* Create a Postgres user 'joe' and password 'joepass'
* Create a schema named 'carriers'
* Grant all permissions on all tables in schema 'carriers' to user 'joe'


```
# su - postgres
$ psql 
psql (8.4.20, server 9.3.5)
WARNING: psql version 8.4, server version 9.3.
         Some psql features might not work.
Type "help" for help.

postgres=# CREATE SCHEMA test;
CREATE SCHEMA
postgres=# CREATE USER joe PASSWORD 'joepass';
CREATE ROLE
postgres=# GRANT ALL ON SCHEMA test TO joe;
GRANT
postgres=# GRANT ALL ON ALL TABLES IN SCHEMA test TO joe;
GRANT
postgres=# CREATE SCHEMA carriers;
CREATE SCHEMA
postgres=# GRANT ALL ON SCHEMA carriers TO joe;
GRANT
postgres=# GRANT ALL ON ALL TABLES IN SCHEMA carriers TO joe;
GRANT
postgres=# \q
-bash-4.1$ exit
logout
```

Because our rails server wants to connect to the local postgres server, we want to make it so that this postgres server trusts all local connectors.  Continuing with our CentOS6 linux, make that trust happen with these lines in this file:

```
cat /var/lib/pgsql/9.3/data/pg_hba.conf|egrep -v "^#"

local   all             all                                     trust
host    all             all             127.0.0.1/32            trust
host    all             all             ::1/128                 trust
```

We become user **postgres** to do the postgres things (because root cannot do them) and restart the server like this:

```
/usr/pgsql-9.3/bin/pg_ctl reload -D /var/lib/pgsql/9.3/data/
```

We also start the rails application as this user.  This isn't necessary because we allowed all local connections in **pg_hba.conf** above.  Even so, rails and postgres are both running as user postgres.  Rails will start the server with the WEBrick http server and we choose port 3002:

```
-bash-3.2$ rails server -p 3002
/usr/local/rvm/rubies/ruby-1.9.3-p547/lib/ruby/1.9.1/yaml.rb:84:in `<top (required)>':
It seems your ruby installation is missing psych (for YAML output).
To eliminate this warning, please install libyaml and reinstall your ruby.
=> Booting WEBrick
=> Rails 4.1.6 application starting in development on http://0.0.0.0:3002
=> Run `rails server -h` for more startup options
=> Notice: server is listening on all interfaces (0.0.0.0). Consider using 127.0.0.1 (--binding option)
=> Ctrl-C to shutdown server
[2016-03-23 14:01:53] INFO  WEBrick 1.3.1
[2016-03-23 14:01:53] INFO  ruby 1.9.3 (2014-05-14) [x86_64-linux]
[2016-03-23 14:01:53] INFO  WEBrick::HTTPServer#start: pid=25061 port=3002
```

At this point, a web browser can find the home page at http://127.0.0.1:3002/carriers/.  This application can now populate the database with records.  We can hit Control-C to stop rails.  Then we can connect to the database with psql and see the new records.  Notice in psql that we must connect to the correct "relation" first.  In rails, according to database.yml, we were populating carriers_dev, where we see there are 27 Japanese_aircraft_carrier.  We also see that there are 0 in our production database:

```
Exiting
-bash-3.2$ pwd
/usr/local/carriers
-bash-3.2$ psql
psql (9.3.5)
Type "help" for help.

postgres=# select * from carriers WHERE carriername LIKE 'Japanese_aircraft_carrier%';ERROR:  relation "carriers" does not exist
LINE 1: select * from carriers WHERE carriername LIKE 'Japanese_airc...
                      ^
postgres=# \c carriers_dev
You are now connected to database "carriers_dev" as user "postgres".

carriers_dev=# select count(*) from carriers WHERE carriername LIKE 'Japanese_aircraft_carrier%';
 count 
-------
    27
(1 row)

carriers_dev=# \c carriers
You are now connected to database "carriers" as user "postgres".
carriers=# select count(*) from carriers WHERE carriername LIKE 'Japanese_aircraft_carrier%';
 count 
-------
     0
(1 row)

carriers=# \q
```

