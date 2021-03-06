---
layout: post
title: I Hope Your Inheritance Isn't An EM
tags:
- css
- ems
- fonts
- ratios
- sizing
---
The web allows users to customize their experience. This can be satisfying for the user and scary for the designer.
Designers often have very specific ideas about how their web pages should look. Phrases like, "pixel perfect" come to
mind. Well, "pixel perfect" font size is limiting to users who want to be able to control the size of their text.

The idea of using units that are dependent on font size instead of pixel size has been around for a very long time now,
yet there are still many designers who don't use ems. I believe it's an inherited problem. In other words, setting the
font-size to two ems in a parent div will give a different result than setting the font-size to two ems in a child div.
This is because the em unit size is inherited through font-size.

Changing the font-size, changes the length of an em, even when it is used in the width or length css properties.

Changing the font-size in a div, means changing the size of an em relative to how big an em is in the parent div. This
new em size will apply not only to font-size, but also to width, height, etc.

Let me demonstrate:

<div style="background-color: #6a94d4; width: 20em; height: 20em; font-size: 2em; line-height: 1.2em; position: relative;">Parent Div:
    Font Size: 2em
    Width: 20em
    Height: 20em
    (Line Height: 1.2em)
        <div style="background-color: #e065bb; width: 20em; height: 20em; font-size: 0.5em; line-height: 1.2em; position: absolute; top: 0; right: 0;">Child Div:
        Font Size: 0.5em
        Width: 20em
        Height: 20em
        (Line Height: 1.2em)
        </div>
</div>

Notice that the width, height, and line height values do not change from one div to the other. The only thing that
changes is the ems.

The font size of the child div is 0.5 em. This means that the font size is simply 1/2 of whatever the parent's font size
is. The new 1/2 sized em units that are used to calculate the size of the letters are also used to calculate the size of
the width, height, and line-height of the child div. This is why all of those are 1/2 the size of their parent div
counter parts.

This is just a simple introduction to how working with EMs....... works. You still have to do the math and deal with the
defaults of browsers.... and IE. Here is some of the nitty gritty in the form of useful links:

* [JavaScript EM calculator](http://riddle.pl/emcalc/) by Piotr Petrus
* [How to Size Text in CSS](http://www.alistapart.com/articles/howtosizetextincss/), by Richard Rutter, from A List Apart
* [Old, slightly broken, but still useful article](http://www.w3.org/WAI/GL/css2em.htm) on the W3C.
