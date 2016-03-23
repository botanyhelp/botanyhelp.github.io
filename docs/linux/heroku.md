## Heroku

Ruby, Rails and Heroku are steep climbs.  They are wonders of elegance and efficiency.  Ruby and rails are in a category with python, linux, git and others among the best software ever created. 

### **Carriers**: Ruby on Rails web application with Postgres database backend running on **heroku**.  
This application is deployable on a local machine using the Rails Webrick http server and a local Postgres database.  The code has the entire application but does not have anything to do with the Postgres database server that it expects is running locally and allowing local connections.  The code does have the capacity to load all of the initial records into the database.  Setting up a local linux postgres database to support this Rails application is described on the [Postgres](/databases/postgres.md) page. 

The code is also ready to be deployed to Heroku.  This application was deployed on Heroku in October 2014 and is running there now at **(be patient for the five second dymo startup)**:

[https://aqueous-bayou-3129.herokuapp.com/carriers/](https://aqueous-bayou-3129.herokuapp.com/carriers/)

All of the code are open source GPLv3 and on github at:

[https://github.com/botanyhelp/Herokucarriers](https://github.com/botanyhelp/Herokucarriers)

..all of the data in the application are thankfully provided by wikipedia editors and shared under this license.

[https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License](https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License)

[https://creativecommons.org/licenses/by-sa/3.0/us/](https://creativecommons.org/licenses/by-sa/3.0/us/)

See also the [ruby](/software/ruby.md) and [postgres](/databases/postgres.md) pages.  
