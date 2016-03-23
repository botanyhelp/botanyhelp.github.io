## Ruby

Ruby and Rails are steep climbs.  They are wonders of elegance and efficiency.  Ruby and rails are in a category with python, linux, git and others among the best software ever created.  The **easy** way to learn Ruby is with Hal Fulton's **The Ruby Way**, then Yukihiro Matsumoto's **The Ruby Programming Language** and finally Obie Fernandez's **The Rails 4 Way**.  If you have never programmed before, then I think Jay McGavren's **Head First Ruby** should be the first book.  Almost everyone that reads these books will become RoR people.  

### Herokucarriers

Ruby on Rails web application with Postgres database backend.  This application is deployable on a local machine using the Rails Webrick http server and a local Postgres database.  The code has the entire application but does not have anything to do with the Postgres database server that it expects is running locally and allowing local connections.  The code does have the capacity to load all of the initial records into the database.  

The code is also ready to be deployed to Heroku.  This application was deployed on Heroku in October 2014 and is running there now at:

[https://aqueous-bayou-3129.herokuapp.com/carriers/](https://aqueous-bayou-3129.herokuapp.com/carriers/)

All of the code are open source GPLv3 and on github at:

[https://github.com/botanyhelp/Herokucarriers](https://github.com/botanyhelp/Herokucarriers)

..all of the data in the application are thankfully provided by wikipedia editors and shared under this license.

[https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License](https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License)

[https://creativecommons.org/licenses/by-sa/3.0/us/](https://creativecommons.org/licenses/by-sa/3.0/us/)

It is possible to setup this application on a local linux box as described on the [Heroku](/linux/heroku.md) and [Postgres](/databases/postgres.md) pages.


### QRCode

QR codes are those things we see everywhere on ads that let mobile phone/camera users snap to take them to a URL. We want them for Facebase posters.
This ruby code creates png formatted images of the QR codes. It also dumps text which can be used to create an HTML/CSS version of the QR code:

```
qrHTMLandPNGmaker.rb
```

That ruby doesn't actually dump HTML, only text with and 'x' character for dark and a "space" character for light. That text output can be used to create HTML/CSS that displays the QR code as an HTML table. This python program reads the output from the ruby program (the text output) and writes HTML/CSS to generate the QR code:

```
qrHTMLmaker.py
```

The ruby requires some modules that are probably not present. Install them with gem like this:

```
gem install rqrcode
gem install rqrcode_png
```

NOTICE that the URLs are **hardcoded into the ruby**.
NOTICE that the file qr.txt produced by the ruby is a **hardcoded input filename** in the python.
The whole thing was run like this:

```
ruby qrHTMLandPNGmaker.rb > rb.txt
python qrHTMLmaker.py > qr_codes.html
```

After running the ruby program, six new 300x300 PNG-formatted images will be created in the current directory. The output HTML from the python can be dropped right into any HTML file and will display the QR codes.

Available on github: 
[https://github.com/botanyhelp/Qrcode](https://github.com/botanyhelp/Qrcode)
