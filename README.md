# LinkHandling
Interpret and create a blog publication like Twitter and Facebook automatically.


![N|Solid](https://i.imgur.com/hb6Tu6l.png)


[![Tweeting](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/sourenkhetcho/) [![Linkedin](https://img.shields.io/badge/Connect-LinkedIn-0E76A8.svg)](https://www.linkedin.com/in/sourenkhetcho/)



LinkHandler is an [https.onCall Firebase function](https://firebase.google.com/docs/functions/callable) which receives the url of the blog published online as its variable and handles the content of the blog in an organized fashion

How the algorithm works:
  1) Receive URL
  2) Analyse the content of the url (main image, title, description, publicaiton date, domain name, etc...).
  3) Retrieve the last stored blog content file from firebase storage bucket.
  4) Decide whether to create a new blog file (which contains multiple blog information) based on specified rules.
  5) Update the new data back to the storage bucket.
  6) Magic!

# Here is how the stored blog info could be presented

![N|Solid](https://i.imgur.com/oKU87EL.png)


# How is the data structured
There is a main file created in the storage bucket called: `blogFileCounter.json` which holds a counter
of the number of blog files (files which hold blogs information). This is used to get the last file created
`blogFileCounter.json`:
```
{
  "key": 2
}
```
Blog files are names as `blogs_xx.json` where `xx` is the file number.

For example, `blogs_31.json` should look something like this:
|Key|
|:-------------:|
|10|

| Blogs[0]        | Blogs[1]|.......| Blogs[9]|
| ------------- |:-------------:|:-------------:|:-------------:|
| title      | title|...| title |
| description|description|...|description|
| image |image|...|image|
| source |source|...|source|
| url |url|...|url|
| date |date|...|date|

### How any why is the data divided
The reasons for dividing the data into separate files are for organization and efficiency purposes. Loading or requesting data for 10 blogs on one page load is manageable. But not 120 blogs at once. This way json data handling is controlled and not flooded at once

the `blogFileCounter.json` will allow us to request the latest pushed blogs on from our front end easily. A `Load More` or autoload on scroll can be introduced with this data devision.
Like this:
- When first 10 blogs load from the last file, you have stored the file counter key value
- `Load More` calls file blogs_(`file counter key` - 1).json, and so on...

**By default, this algorithm creates a new file and increments the file counter every time the last file contains 10 blogs' information.**
### Installation

LinkHandler requires [Node.js](https://nodejs.org/), [Firebase](https://firebase.google.com/) to run.

Procedure:
```sh
$ git clone https://github.com/skhetcho/LinkHandling.git
```
*You will get the index.ts file which you can copy paste in your firebase project*
**Enjoy!**

License
----

MIT


**Open Source Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
