## niceplots

### Example

![example](example.png)


This is a single file PHP script that you can plop into a directory full of images to nicely
format them on a page so that they are searchable and sortable. Searching supports regex and is
live! Some Vim keybindings are also provided.

By default, browser-friendly images (png, svg, gif) are displayed, and if a pdf version of the file
(same name with "pdf" extension) exists, the images are links to those.

### "Installation"

#### With web server 

Literally just copy `index.php` into a web directory that supports PHP.

#### Local testing

For usage on a laptop, for example, when you don't want to bother setting up an Apache
web server, you can use python's `SimpleHTTPServer` to display the HTML page
after executing the php script with `php`. If you can't `which php`, then tough luck.

```bash
cp index.php testplots/
cd testplots
php index.php > test.html
python -m SimpleHTTPServer
# navigate to http://localhost:8000/test.html
```

#### Helper script for image conversion

Often, you'll make a billion pdf images from a script and you want to (1) convert 
them all the png and (2) upload them to a directory with the niceplots index page.
That's where `niceplots.sh` comes in. Note that this script is basically a template,
as these operations are highly dependent upon your configuration/computer, 
so assume you will need to modify many parts.

### Features

* regex searching with live pattern matching for instant feedback
  * patterns are case-insensitive until an upper-case character is typed (vim `set smartcase`)

* tree-viewer (supporting shift click for multiple selection/filtering, through `jstree`) becomes
available when there is at least one subdirectory with content

* copy URL (+search patterns) to clipboard

* zoomable plots

* vim-like keybindings 
  * `G` to go to bottom
  * `g` to go to top
  * `/` to focus the search box
  * `y` to copy the contents as a URL
  * `s` to sort A-Z
  * `S` to sort Z-A

Here are some lesser known features. Note that "[hacky/hardcoded]" means "look at the source and modify it
because I didn't care enough to code it generally".

* if a `description.txt` file is found inside the folder with images, the contents are displayed (as HTML)
at the top of the final page.
  * if an image name (sans extension) shows up in the description, it is highlighted and becomes a link to the corresponding image

* if files with the same name as the image, but extensions of `txt`, `extra`, `json` are found, they become links
  * hovering over links for `txt` and `extra` will show the contents in a transient overlay at the bottom of the page
  * [hacky/hardcoded] links for `json` will link to jsROOT

* [hacky/hardcoded] when a `binInfo.json` file is provided (keys are image names without extensions, values are dicts with x and y edges
(as fractions of the plot width and height), bin information, etc. (from [matplottery](https://github.com/aminnj/matplottery/tree/master/matplottery)) will display bin contents and highlight bins on mouseover
