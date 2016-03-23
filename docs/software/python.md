## Python

Python is the best programming language to learn for almost everyone.  Its beauty, easy, ubiquity, power and quality make it so.  The best book for learning python hasn't been written yet.  Experienced programmers might like Mark Pilgrim's Dive Into Python and/or Dive Into Python 3.  Newer programmers should possibly start with Luciano Ramalho's Fluent Python.  Mark Lutz's Learning Python and Programming Python and Paul Barry's Head First Python are good books but are **not** for learning python.  Almost everyone agrees that new learners should learn **python 3** instead of python 2. 

### Google App Engine Wisconsin Herbarium

Python web application running on Google App Engine infrastructure at:

[http://wisconsinherbarium.appspot.com/](http://wisconsinherbarium.appspot.com/)

..all of the code is open source and available at:

[https://github.com/botanyhelp/Herbpythonappengine](https://github.com/botanyhelp/Herbpythonappengine)


### Python web application **Fix AM FM**

..deployed and running on Google App Engine infrastructure at:

[http://fixamfm.appspot.com/](http://fixamfm.appspot.com/)

..all of the code is open source and available at:

[https://github.com/botanyhelp/fixamfm](https://github.com/botanyhelp/fixamfm)

The application allows visitors create song requests to any/every radio station in America.  There is a modest "captcha" system to fend off robots.

### Albumartmaker

Python program to read text and create a 300x300 image file of the text. 

Album art are those things you see on the ipod when playing a song.  Its 
part of the ID3 tag system of mp3 files.  Circa 2010 ipods displayed 300x300 
png files nicely.  This program only makes the 300x300 image file.  The 
text to be put into the image (and many other details) are hardcoded into 
the program.  It would be most useful with many MP3 files where you know 
the text you want to put into the image.  If your MP3 has six songs in it 
and you want to make an image with 6 artist/album/song listings, then this 
program can do it.  Notice that this program will only create the image file. 
You'll need another program to push it into your existing MP3 file's tag. 

You can test it like this:

```
python piller2.py
```

...and you will have a new PNG file in the current directory:

test.png

Requires modules Image, ImageDraw, and texwrap
Will use ImageFont if you have them (/usr/share/fonts/bitstream-vera/Vera.ttf)

Code is open source and available on github:

[https://github.com/botanyhelp/Albumartmaker](https://github.com/botanyhelp/Albumartmaker)

### Searchyumrepos

Search yum software repositories for your list of software.

Code is open source and available on github:

[https://github.com/botanyhelp/Searchyumrepos](https://github.com/botanyhelp/Searchyumrepos)

Here we run it and learn that this linux machine does not have the remi repository installed.  You will need to edit the python to add your list of repositories, which are hardcoded. 

```
python searchyumrepos.py anaconda
ABOUT TO RUN THIS COMMAND:

yum list --enablerepo=epel --enablerepo=remi --enablerepo=rpmforge --enablerepo=atrpms --enablerepo=R-project anaconda
Loaded plugins: fastestmirror, refresh-packagekit, security


Error getting repository data for remi, repository not found
```

### Gmailer

Gmailer is a short python script to use gmail to send email

[https://github.com/botanyhelp/Gmailer](https://github.com/botanyhelp/Gmailer)

### Ucscdiskspacer

Program to report total size, in bytes, of UCSC genome browser databases
It is useful to estimate how large the databases are before you download. 

Use it like this for a zebrafish and human assembly:

```
python ucsc_disk_spacer.py danRer5 hg19
```

Available on github:

[https://github.com/botanyhelp/Ucscdiskspacer](https://github.com/botanyhelp/Ucscdiskspacer)

### Ucscquery

Python standalone program to query UCSC Genome Browser Mysql database

*Requires module MySQLdb
*Requires internet access

Hardcoded username and database.  Only the database will need to be changed by you...you would change 'mm9' to 'hg19' if you want to change from Mouse to Human organism. 

This program performs steps that can be run manually like this:

```
mysql --user=genome --host=genome-mysql.cse.ucsc.edu -A
mysql> use mm9;
Database changed
mysql> select * from knownCanonical;
```

The UCSC Genome Browser provides a public mysql server.  Python program ucscquery.py shows how to query that server.  The public server, username and password are embedded in the program.  There are hundreds of databases, one for each assembly.  The program hardcodes the mm9 assembly of the Mouse organism.  The query execution returns a long, which we promptly convert to an int.  We then use that to fetch every record one at a time in a loop.  Understanding the databases and their tables is not easy.  The schema is designed primarily to support the genome browser at genome.ucsc.edu.  Even so, clever querying is possible.  Good luck.

Code available on github:

[https://github.com/botanyhelp/Ucscquery](https://github.com/botanyhelp/Ucscquery)


### Botitwebmaker

Python program that generates HTML web site from a directory of image files.  Generates the content found here:

[http://botit.botany.wisc.edu/](http://botit.botany.wisc.edu/)

The README documentation for botitwebmaker is 
embedded in the program itself.  Running it 
can be done by placing the program in the 
root directory of a directory tree of image 
files.  The (only!) website that uses it can 
be found here: http://botit.botany.wisc.edu/


Code available on github:

[https://github.com/botanyhelp/Botitwebmaker](https://github.com/botanyhelp/Botitwebmaker)

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

NOTICE that the URLs are hardcoded into the ruby.
NOTICE that the file qr.txt produced by the ruby is a hardcoded input filename in the python.
The whole thing was run like this:

```
ruby qrHTMLandPNGmaker.rb > rb.txt
python qrHTMLmaker.py > qr_codes.html
```

After running the ruby program, six new 300x300 PNG-formatted images will be created in the current directory. The output HTML from the python can be dropped right into any HTML file and will display the QR codes.

Available on github: 
[https://github.com/botanyhelp/Qrcode](https://github.com/botanyhelp/Qrcode)

### Python web application **Fix WDC**

..deployed and running on Google App Engine infrastructure at:

[http://fixwdc.appspot.com/](http://fixwdc.appspot.com/)

fixwdc allows you to send a request to any congressional district in America. Any representative can monitor the requests that are made. Please be respectful.  

This application stores all submissions in the Google Data Store associated with this application.  Because login is not required, a very tedious automated system is in place to censor and eliminate 
