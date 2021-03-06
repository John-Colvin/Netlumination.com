---
layout: post
title: JQuery for a little night time reading
tags:
- framework
- javascript
- jquery
- source code
status: publish
type: post
---
If you use Javascript, <a href="http://jquery.com/">JQuery</a> is a great framework to speed up your coding. It's
essentially a collection of really convenient shortcuts. It does more, since JQuery also handles a lot of browser
compatibility issues. So, you don't have to go through your JQuery code to update it for new browsers, all you have to
do is download the new version of JQuery, and your old commands will learn new tricks.

Ah, speaking of downloading JQuery, you just might want to understand how JQuery works if you use it. The first time I
tried to do this, I simply clicked on my JQuery src file link:

``` html
<script type="text/javascript" src="http://peter-ajtai.com/jquery/jquery-1.4.2.min.js"></script>
```

... and this is what I saw:

<img class="alignnone size-full wp-image-1243" title="Happy reading" src="http://img.netlumination.com/wall-o-text.jpg" alt="Wall o text JQuery" width="419" height="323" />

Fun reading, huh? <!--more-->Well, when your browser loads Javascript, it has to load each charachter, so the less
whitespace there is, and the shorter the variable names are, the faster it will load.

This means you should be using this, the minified, version of JQuery on your site, but if you want some
<del>pleasant and relaxing</del> reading... you should look at the uncompressed version.
<a href="http://docs.jquery.com/Downloading_jQuery">JQuery shows you both versions very clearly on their download page</a>,
but for some reason, it took me a while to realize that there is an uncompressed version. The
<a href="http://code.jquery.com/jquery-latest.js">uncompressed version of the latest version is here</a>. The
uncompressed version is actually very readable:

<img class="alignnone size-full wp-image-1244" title="That's better" src="http://img.netlumination.com/readable.jpg" alt="Readable JQuery" width="423" height="352" />
