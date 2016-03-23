# Content

Creating content nowadays means the mobile web and isn't getting easier.  These books are good:

* Mobile HTML5 by Estelle Weyl
* Head First HTML and CSS, 2nd Edition by Elisabeth Robson, Eric Freeman

Creating content with markdown is easier.  Using markdown you can let software write the HTML, CSS and javascript and create the PDF and MSWord document for you.  Content creation happens sooner and life is better with markdown.  [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

## Multilingual and left to right HTML

This page should work on every modern web browser.  It displays the hebrew language and instructs the browser to present it using a right-to-left reading orientation which is proper for right to left languages like hebrew.  This is achieved with the dir attribute of the html element.  

```
<html lang="he" dir="rtl">
```

Notice in your browser that it **selects** the text using the right to left orientation, not like with English and other left to right languages:

[https://github.com/botanyhelp/Agemakeroffline/blob/master/hebrew.html](https://github.com/botanyhelp/Agemakeroffline/blob/master/hebrew.html)

Notice that the left right to left will only work if you save the file and then look at it in your browser, or if you install the hebrew.html file onto a web server.  You can see online here:

[http://www.pitt.edu/~twm11/hebrew.html](http://www.pitt.edu/~twm11/hebrew.html)

This page, one page of HTML, shows two languages using the lang attribute at the element level:

[https://github.com/botanyhelp/Agemakeroffline/blob/master/russian.html](https://github.com/botanyhelp/Agemakeroffline/blob/master/russian.html)

You can see online here:

[http://www.pitt.edu/~twm11/russian.html](http://www.pitt.edu/~twm11/russian.html)

That page sets the lang attribute of an element three times on that page like this:

```
<title lang="ru">
<p lang="ru">
<p lang="en">
```

## Offline web application: Agemaker age calculating web page.

[http://www.pitt.edu/~twm11/agemaker.html](http://www.pitt.edu/~twm11/agemaker.html)

The application logic is written in Javascript and uses the entered birthdate to calculate the current age to one decimal place.  This application is useful for researchers that wish to record the present age of participants (instead of entering a birthdate and current date).  Sometimes the current age is the desired value.  This web application also has the benefit of being an offline web app.  Therefore, when you revisit this URL later, when you have no Internet connection, it still works (on all modern web browsers).  It also has the benefit of not recording or transmitting any data. 

The javascript, HTML5 and everything is in one file, agemaker.html, available on github:
 
[https://github.com/botanyhelp/Agemakeroffline](https://github.com/botanyhelp/Agemakeroffline)

