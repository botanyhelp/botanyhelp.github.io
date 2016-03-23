## Php

PHP is best learned [on the web](http://www.php.net/docs.php) and with these books:

* PHP Cookbook, 3rd Edition by David Sklar, Adam Trachtenberg
* PHP: The Good Parts by Peter MacIntyre

### Laravelcarriers

Simple writable database program runnning on Laravel php web framework. 

Code available on github:

[https://github.com/botanyhelp/Laravelcarriers](https://github.com/botanyhelp/Laravelcarriers)

Laravel shoves the whole http web server and mysql database server into itself.  All of the github code provides the application and the data.  With a suitable php installation, you can get the whole LAMP thing showing up in your browser here: http://localhost:8000/carriers/

..all of the data in the application are thankfully provided by wikipedia editors and shared under this license.

[https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License](https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License)

[https://creativecommons.org/licenses/by-sa/3.0/us/](https://creativecommons.org/licenses/by-sa/3.0/us/)

### Zipper

zipper.php is a php program that creates zip archives. 

Available on github:

[https://github.com/botanyhelp/Zipper](https://github.com/botanyhelp/Zipper)

It requires that the ZipArchive class be available: 
http://www.php.net/manual/en/class.ziparchive.php

...you'll get a hang or error if it does not.  

The program also hard codes the input files and output zip PATH. 

You need to edit those lines or create /tmp/one.txt, /tmp/two.txt, /tmp/three.txt and then look for /tmp/onetwothree.zip

Modify it to suit your zipping requirements. 

### Phpuploader

PHP script to upload files to web server.

Requires you to **alter hardcoded directory paths**.
Should password protect so that strangers don't upload and fill your disk. 

With PHP setup properly for very large uploads, this program has done it.  It is still running in production to allow nature photographer uploads. 

Available on github:

[https://github.com/botanyhelp/Phpuploader](https://github.com/botanyhelp/Phpuploader)


