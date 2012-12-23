xkcd-php
========

A simple wrapper of the [XKCD API](http://xkcd.com/json.html) (yes, the comic) written in PHP with caching support.

The wrapper
--------
There are two classes in this wrapper, `xkcd`(the main API wrapper) and `xkcdcomic`(the comic object). To initalize the wrapper, use:
```php
<?php
include('xkcd.php'); //Load the wrapper
$xkcd = new xkcd(); //Initalize the wrapper. The wrapper will make a request to the XKCD API to fetch the latest comic and store it in the cache.
```
To get a comic, try:
```php
$comic = $xkcd->get(327); //get the comic #327, Exploits of a Mom.
echo '<h1>'.$comic->safe_title.' - xkcd</h1>'; //prints the title
echo "<img src=\"{$comic->img}\" title=\"{$comic->alt}\"/>"; //prints the image (don't miss the hover text!)
echo '<h2>Transcript</h2><pre>'.$comic->transcript.'</pre>';
echo "<h2>Full version</h2><a href=\"{$comic->url}\">{$comic->url}</a>";
```
You will get a neat page containing the comic's title, image, transcript(if avaliable) and an URL of the original xkcd page.

As a note, xkcd-php automatically stores fetched information in the cache. To change the limitation of the number of the chche entries, use something like:
```php
$xkcd->cachelimit = 10; //change the cache limitation to 10
```
To clear the cache, use:
```php
$xkcd->clearcache();
```

Functions
--------
There are a number of functions in the wrapper, including:
* `xkcd->refresh()`: Reload the linformation of the latest comic
* `xkcd->get($num)`: Get a comic object by the comic's ID (the number on the permalink of the comic, like 327)
* `xkcd->random()`: Get a comic object of a random comic
* `xkcd->latest()`: Get a comic object of the latest comic
* `xkcd->clearcache()`: Clear the internal cache

* `xkcdcomic->next()`:Get a comic object of the next comic
* `xkcdcomic->prev()`:Get a comic object of the previous comic

Properties
--------
The class `xkcdcomic` has properties with information of the comics. These are:

### Properties defined internally in the XKCD API
* `year`: The year the comic was released in
* `month`: The month the comic was released in
* `day`: The day in month the comic was released on
* `num`: The ID of the comic
* `title`: The title of the comic
* `safe_title`: The safe title of the comic
* `transcript`: The transcript of the comic (if avaliable)
* `alt`: The hover text
* `img`: The URL to the comic image

### Properties defined in the wrapper
* `url`: The URL of the original comic page on xkcd.com

Licensing
--------
`xkcd-php` is licensed under the GNU General Public License.