## Google App Engine

Google App Engine is much like Ruby on Rails in these ways:

* GAE is hard to get started but really easy once you learn. 
* GAE applications can be simple with few lines of code and favor convention over configuration. 
* GAE applications can be indestructably scaled up. 

Only GAE has the [google_data_store](/databases/google_data_store/)

### Python web application **Wisconsin Herbarium** 

..deployed and running on Google App Engine infrastructure at:

[http://wisconsinherbarium.appspot.com/](http://wisconsinherbarium.appspot.com/)

..all of the code is open source and available at:

[https://github.com/botanyhelp/Herbpythonappengine](https://github.com/botanyhelp/Herbpythonappengine)

The application allows visitors to search and view data and images found in the Wisconsin Herbarium.

### Python web application **Fix AM FM** 

..deployed and running on Google App Engine infrastructure at:

[http://fixamfm.appspot.com/](http://fixamfm.appspot.com/)

..all of the code is open source and available at:

[https://github.com/botanyhelp/fixamfm](https://github.com/botanyhelp/fixamfm)

The application allows visitors create song requests to any/every radio station in America.  There is a modest "captcha" system to fend off robots.  

### Python web application **Fixwdc** 

..deployed and running on Google App Engine infrastructure at:

[http://fixwdc.appspot.com/](http://fixwdc.appspot.com/)

The application allows visitors to send letters to the representative of every congressional district in America.  There is a modest "captcha" system to fend off robots.  There is also a complex automated censorship process on the server that aspires to delete offensive communications.  Because login is not required, users can try to send nasty letters anonymously.  Humans are generally required for censorship but humans are expensive.  Therefore, this application does its best to delete offensive communications.  The censorship system uses many techniques and sources including this list of [bad words](http://www.cs.cmu.edu/~biglou/resources/bad-words.txt) generously shared by Big Lou.  The censorship is fallible.  It is possible to get nasty letters through and it is very likely that a nice letter will get some censoring.  The [Fixwdc](/software/android.md#Fixwdc) android application communicates with this application.  Fixing Washington and nasty letters are two ambitious goals of this code. 


