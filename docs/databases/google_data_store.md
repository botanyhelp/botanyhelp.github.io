## Google_data_store

The place to learn about the Google Data Store is right along with Google App Engine in one of these books:

* Programming Google App Engine with Python by Dan Sanderson
* Programming Google App Engine with Java by Dan Sanderson

Hopefully [Dan](http://www.dansanderson.com) will deliver **Programming Google App Engine with Go** soon.  The Google Data Store is strange.  Its also the most powerful data persistence system available.  It has the interesting property that, to quote the book above: **"the performance of an index-backed query is not affected by the number of entities in the datastore"**.  That means that your query on 10billion records is just as fast as a query on 10 records.  Now you know why google is fast no matter how big the Internet gets. 

These three App Engine apps use the Google Data Store for persistence:

[http://fixwdc.appspot.com/](http://fixwdc.appspot.com/)

[http://fixamfm.appspot.com/](http://fixamfm.appspot.com/)

[http://wisconsinherbarium.appspot.com/](http://wisconsinherbarium.appspot.com/)

..and have the code available on github:

[https://github.com/botanyhelp/](https://github.com/botanyhelp/)

See also the [Google App Engine](/linux/gae.md) page. 
