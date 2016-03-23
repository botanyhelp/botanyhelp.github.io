## Javascript

Learning Javascript should be done with these two books, read in this order:

* Head First JavaScript Programming by Eric T. Freeman, Elisabeth Robson
* JavaScript: The Good Parts by Douglas Crockford

Javascript libraries like jQuery are often useful.  However, you might find that life is better when you keep your web pages simple, use Javascript purposefully, and write it yourself without libraries.  Do prefer to become a javascript programmer (instead of, for example, a jQuery programmer).  This style of **avoiding javascript libraries** is a style, not a religion.  Many javascript libraries target a specific functionality.  When you need such functionality, using such libraries will boost the quality and performance of your code and save you lots of time and effort.  One example of such a library is Lea Verou's awesomplete, which is totally awesome. 

### Awesomplete javascript autocompletion with 28510 gene symbols

Lea Verou's [Awesomplete](https://leaverou.github.io/awesomplete/) is an easy to use and totally awesome little javascript library.  

This [short web form](/rawHTML/gene.html) selects and displays candidate gene symbols that you start typing with auto-completion.  It selects candidate gene symbols from a long list of 28510 genes.  This javascript was used to limit form submissions to only the list of genes that will be considered by Michigan's excellent [locuszoom](http://locuszoom.sph.umich.edu/locuszoom/) program.

Code is available on github:

[https://github.com/botanyhelp/Agemakeroffline/blob/master/gene.html](https://github.com/botanyhelp/Agemakeroffline/blob/master/gene.html)

### UCSC Genome Browser dynamic custom track documentation

Adding dynamic javascript to a UCSC genome browser custom track documentation file is possible.  This particular javascript uses the specific location on the genome where the user was browsing to decide what links to display on the documentation page.  This strategy would be useful for a single custom track that represents dozens of experimental units across dozens of URLs.  

This HTML/Javascript file can be used as dynamic documentation with a local track on the UCSC genome browser at genome.ucsc.edu.  The javascript makes an AJAX request to fetch a JSON formatted data file, which it parses and uses to manage the display of the documentation for the local track.  Very large local track files that span wide areas of the genome may want the documentation to change depending on where the current genome browser visitor is on the genome.  This experimental Javascript achieves that by finding the location being viewed, finding the interesting locations (via AJAX fetch of JSON datafile), and dynamically displaying the documentation that is relevant. 

Code is available on github:

[https://github.com/botanyhelp/Gbjavascript](https://github.com/botanyhelp/Gbjavascript)

### Agemaker age calculating web page.

[http://www.pitt.edu/~twm11/agemaker.html](http://www.pitt.edu/~twm11/agemaker.html)

The application logic is written in Javascript and uses the entered birthdate to calculate the current age to one decimal place.  This application is useful for researchers that wish to record the present age of participants (instead of entering a birthdate and current date).  Sometimes the current age is the desired value.  This web application also has the benefit of being an offline web app.  Therefore, when you revisit this URL later, when you have no Internet connection, it still works (on all modern web browsers).  It also has the benefit of not recording or transmitting any data. 

The javascript, HTML5 and everything is in one file, agemaker.html, available on github:
 
[https://github.com/botanyhelp/Agemakeroffline](https://github.com/botanyhelp/Agemakeroffline)
