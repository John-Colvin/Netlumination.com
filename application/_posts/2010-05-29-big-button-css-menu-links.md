---
layout: post
title: Big Button CSS Menu Links
tags:
- css
- highlight
- hover
- menu
- tutorial
status: publish
---

This post will show you how to make this:

<div id="da-body4">
<ul id="da-menu4">
	<li><a href="http://peter-ajtai.com/examples/html/menu-good.html">Home</a></li>
	<li><a href="http://peter-ajtai.com/examples/html/menu-good.html">Gnome</a></li>
	<li><a href="http://peter-ajtai.com/examples/html/menu-good.html">Rome</a></li>
</ul>
</div>

Notice that the entire highlighted area is clickable, not just the lettering.<!--more-->

I'll describe a simple way to make pure CSS menu links that highlight nicely when hovered over. Now, you can obviously
get a lot fancier with Javascript, but a good website design degrades nicely. This means that you should stack as much
 functionality into the (X)HTML and CSS as you can, and then add extras on with Javascript. This will enable you to read
 the page nicely through the widest range of media. This is important these days when you don't know whether your
 visitors are using a cell phone, iPAD, curl on a UNIX shell, text reader for the vision impaired, or whatever. There
 are obviously some things Javascript is great for, but there's no need to kill a fly with an elephant gun. Don't use it
 when you don't have to.

The <a href="http://www.w3.org/">W3C</a> page has a nice example of elegant page degradation when Javascript is turned
 off. The menu links on the left hand side of the page, for example the ones under standards, flash dark gray before
 settling to light gray when hovered over. The flash is Javascript. When you
 <a href="http://noscript.net/">turn Javascript off</a>, notice that the flash is gone, but the links are still
 highlighted in the same way. You can click anywhere in the Menu box to follow the link, not just over the lettering,
 and the entire menu box is highlighted in light gray.

Ok let's build a similar but simpler vertical menu. Horizontal menus are easier to highlight, since the horizontal width
of each box can vary without having the menu look unnatural.

Our menu will have three items: Home, Gnome, and Rome. It often makes sense to put your menu items in an unordered list,
so we'll do that, and we'll set a fixed with for the items. We'll use a 440 px body width and 220px menu width, just so
you can easily see the results as displayed in this blog.

Ok, let's set up the menu with simple highlighting using "a:hover".

<div id="da-body">
<ul id="da-menu">
	<li><a href="http://peter-ajtai.com/examples/html/menu-bad.html"> Home</a></li>
	<li><a href="http://peter-ajtai.com/examples/html/menu-bad.html"> Gnome</a></li>
	<li><a href="http://peter-ajtai.com/examples/html/menu-bad.html"> Rome</a></li>
</ul>
</div>

You can take a look at the menu above <a href="http://peter-ajtai.com/examples/html/menu1.html">on its own page</a>.
Here is what that code looks like (remember to use style sheets; I used a style definition in head, so that all the code
could be read easily in one go, but unless you like to individually and tediously change CSS rules one at a time for
 hundreds or thousands of pages, you'd better use external style sheets):

<a href="http://peter-ajtai.com/examples/html/menu-bad.html">Bad Hover Menu</a>

``` html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <style type="text/css">
        #da-body {
            background-color:#A6734A;
            width:440px;
        }
        #da-menu {
        list-style-type:none;
        width:220px;
        }
        div#da-body ul#da-menu li a {
        font-size:180%;
        line-height:220%;
        color:#FAEAF3;
            text-decoration:none;
        }
        div#da-body ul#da-menu li a:hover {
        background-color:#BFB6AF;
        }
    </style>
    </head>
    <body>
    <div id="da-body">
        <ul id="da-menu">
        <li><a href="#">Home</a></li>
        <li><a href="#">Gnome</a></li>
        <li><a href="#">Rome</a></li>
        </ul>
    </div>
    </body>
</html>
```

If you hover over a link, the background changes in color. Yeah, but it's not very elegant, since the area that's
highlighted has a different shape for each link. Additionally, you have to be pretty precise with you mouse. The list
takes up half the colored area, but you have to hover directly over letters in order to follow a link. Let's deal with
the first problem first.

It turns out that :hover is a valid pseudo class for a list item not just a. So if we change the a:hover code to
`li:hover` like this:

``` css
<pre>div#da-body2 ul#da-menu2 li:hover {
    background-color:#BFB6AF;
}</pre>
```

We'll see this:

<div id="da-body2">
<ul id="da-menu2">
	<li><a href="http://peter-ajtai.com/examples/html/menu-blah.html"> Home</a></li>
	<li><a href="http://peter-ajtai.com/examples/html/menu-blah.html"> Gnome</a></li>
	<li><a href="http://peter-ajtai.com/examples/html/menu-blah.html"> Rome</a></li>
</ul>
</div>

Now we're getting close. The problem is that you cannot click the entire highlighted area to follow the link. This is
because we're highlighting the li element and not the a element. Ok, well how about:

``` css
/* THIS WILL NOT WORK!!! */
div#da-body2 ul#da-menu2 a {
    width:100%
}
div#da-body2 ul#da-menu2 a:hover {
    background-color:#BFB6AF;
}
/* ^^ INCORRECT */</pre>
```

Nope, that'll basically just look like the first example. The problem is that the "a" element cannot have a width
attribute. It's not a block level element. You can't set it's width normally.

Don't you wish we could simply display the anchor element like a block item, in this case like a list item, and then we
could set its width. Well, CSS knows about inheritance, and there is a display attribute. We just have to force the "a"
or anchor tag to act different than usual using, "display:inherit;". This means that the "a" tag will inherit whatever
display mode its parent element has. In this case it will will inherit the "block" display from the li element. So, our
solution is:

``` css
div#da-body ul#da-menu a {
    display:inherit;
    width:100%
}
div#da-body ul#da-menu a:hover {
    background-color:#BFB6AF;
}
```

This will produce:

<div id="da-body3">
<ul id="da-menu3">
	<li><a href="http://peter-ajtai.com/examples/html/menu-good.html">Home</a></li>
	<li><a href="http://peter-ajtai.com/examples/html/menu-good.html">Gnome</a></li>
	<li><a href="http://peter-ajtai.com/examples/html/menu-good.html">Rome</a></li>
</ul>
</div>

Incidentally, "display:block" will work too. To wrap up, here is the full code:

<a href="http://peter-ajtai.com/examples/html/menu-good.html">Good Hover Menu:</a>

``` html
<pre><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <style type="text/css">
            #page {
                background-color:#A6734A;
                width:440px;
            }
            #menu {
                list-style-type:none;
                width:220px;
                padding:0;
                margin:0;
            }
            div#page ul#menu li {
                padding:0;
                margin:0;
            }
            div#page ul#menu li a {
                display:inherit;
                width:100%;
                font-size:180%;
                line-height:220%;
                color:#FAEAF3;
                text-decoration:none;
                text-indent:0.5em;
            }
            div#page ul#menu li a:hover {
                background-color:#BFB6AF;
            }
        </style>
    </head>
    <body>
        <div id="page">
            <ul id="menu">
                <li><a href="#">Home</a></li>
                <li><a href="#">Gnome</a></li>
                <li><a href="#">Rome</a></li>
            </ul>
        </div>
    </body>
</html></pre>
```

Incidentally, you can see that I've got a few margin:0s and padding:0s thrown in to make things look neater. Instead of
 dealing with zeroing the margins, paddings, etc. for each item one by one, you can simply use a
 <a href="http://meyerweb.com/eric/tools/css/reset/">CSS reset</a>. You can put this at the top of your style sheet, or
 add it in as a separate style sheet. I didn't use a CSS reset for this example, since I wanted to keep the code as self
 contained as possible.

Ok, that's all the hovering over CSS menus for today.
