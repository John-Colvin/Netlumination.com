---
layout: post
title: Bite Sized Emacs
tags:
- Emacs
- reference
- tips
---

Emacs is a big complicated beast. You can spend lots of time  looking through the documentation, but sometimes it's nice
to enjoy a quick bite of Emacs goodness.

### Table of Contents

1. [Custom Keystrokes](#keystrokes)
1. [Indenting only as far as you feel comfortable](#indentation1)
1. [Indentation on steroids](#indentation2)
1. [Colorful shells](#color)
1. [Colorful men](#woman)
1. [No more beeping, only flashing](#beep)
1. [Turn off annoying menu bar](#menu)
1. [Customizing font appearance](#font)
1. [Line wrapping on horizontally split windows](#wraps1)
1. [Normal looking line wraps](#wraps2)
1. [Auto backup a little smarter](#backup)
1. [Autocomplete](#complete)
1. [Jumping the line](#jump)
1. [Moving from one window to the other easilly](#move)
1. [Delete the entire word](#delete)
1. [Enabling the Num Pad](#num)
1. [Making and storing macros](#macros)
1. [Word Count](#count)

### <a name="keystrokes">Morsel 1 - Custom keystrokes</a>

<a href="http://netlumination.com/blog/three-steps-to-making-a-custom-keystroke-shortcut-in-emacs">Make your own custom
keystrokes.</a>

### <a name="indentation1">Morsel 2 - Indenting only as far as you feel comfortable</a>

Change the indentation rules in cc-mode to as many spaces as you want (I use 4, which looks like normal tabs on other
editors, some people use 8, or 2, or whatever).

Edit your .emacs.d/init.el (<a href="http://www.gnu.org/software/emacs/manual/html_node/emacs/Init-File.html">depending
it could be ~/.emacs, ~/.emacs.el, or ~/.emacs.d/init.el</a>) like this (substitute the number you want where I write
4):

{% highlight cl %}
;; define indents as 4 spaces in cc-mode
(setq c-basic-offset 4
      tab-width 4
      indent-tabs-mode t)
{% endhighlight %}

The first line (setting c-basic-offset) does most of the work usually. The other two lines deal with how big tabs show.

You can change the c indentation style using <span style="font-family: Consolas, Monaco, 'Courier New', Courier,
monospace; line-height: 18px; font-size: 12px; white-space: pre;">(setq c-default-style "[style name here]")</span>.
These styles include bsd,stroustrup, etc. Look at the <a href="http://www.emacswiki.org/emacs/IndentingC">Emacs wiki
about indentation in C style</a>.

### <a name="indentation2">Morsel 3 - Indentation on steroids</a>

Indent an entire block of code according to applicable rules by selecting the code and then typing "C-M-\".
For example, let's say you just changed c-basic-offset to 4 from 8. Or you changed the c-default-style. If you now start typing a new program, then the new rules will be in effect. But, when you open a program you've been working on, the parts already written will look unchanged. Here's the step by step as to what you type (remember C = Control key and M = Meta key... usually the Alt key):

    C-x [
    C-SPACE
    C-x ]
    M-w
    C-M-\

And now your entire code is indented according to the new rules! Translation of steps

1. `C-x [` is beginning of file.
2. `C-SPACE` is set mark for region.
3. `C-x ]` is end of file.
4. `M-w` is copy or mark regin.
5. `C-M-\` is indent entire marked region according to applicable rules.

### <a name="color">Morsel 4 - Colorful shells</a>

Show the colors properly in shell mode.

{% highlight cl %}
;; Deal with colors in shell mode correctly
(add-hook 'shell-mode-hook 'ansi-color-for-comint-mode-on)
{% endhighlight %}

You know you need this if you got to shell mode in Emacs (M-x shell) and you see something like `^[[1;37m091`.

### <a name="woman">Morsel 5 - Colorful men</a>

To read the Unix / Linux man pages in Emacs just type:

    M-x man

Then the name of the command of interest. If you want to look at the manual pages in color, type (I mentioned this in
my <a href="http://netlumination.com/blog/a-completely-random-guide-to-emacs">Completely Random Guide to Emacs</a>)

    M-x woman

If you want the F1 key to bring up the woman pages, that is, manual pages in color, then add this to your
`.emacs.d/init.el`

{% highlight cl %}
(global-set-key [f1] ‘woman)</pre>
{% endhighlight %}

### <a name="beep">Morsel 6 - No more beeping, only flashing</a>

Turn off the audible Emacs warning, but have your screen flash when it would have sounded:

{% highlight cl %}
;; Turn off bell, but make it visible
(setq visible-bell t)
{% endhighlight %}

### <a name="menu">Morsel 7 - Turn off annoying menu bar</a>

Turn off the menu bar at the top of the screen:

{% highlight cl %}
;; Turn off menu bar at top of screen
(menu-bar-mode -1)
{% endhighlight %}

You can also do the same thing with the tool bar if you have that:

{% highlight cl %}
(tool-bar-mode -1)
{% endhighlight %}

You can toggle these back on or off by typing

{% highlight cl %}
M-x menu-bar-mode or M-x tool-bar-mode
{% endhighlight %}

### <a name="font">Morsel 8 - Customizing font appearance</a>

Change font appearance (this will often be useful using a major mode for a programming language or text type):
<pre>M-x customize-face</pre>
If you hit enter and enter again to pick the default, you'll be able to change the default appearance of the face that is used to show the word type you we're on (comment, string, keyword, etc.). Your changes will automatically be saved to .emacs.d/init.el, so you'll be able to see how the changes were done.

<strong><a name="wraps1"></a>Morsel 9 - Line wrapping on horizontally split windows</strong>

Usually line wrapping is on by default. You can see it is when a line comes to the edge of the screen, the '\' is shown and the line continues one below. If the line is truncated on the other hand, you won't be able to see the rest of the line, you'll only be able to see a '$'. You can use <a href="http://www.emacswiki.org/emacs/TruncateLines">truncate lines</a> to toggle back and forth between the wrap and truncate states by typing (this will be local to that buffer):
<pre>M-x toggle-truncate-lines</pre>
The tricky thing is that horizontally split windows (windows split by a vertical line) will still truncate. One line in your .emacs.d/init.el will let you wrap lines for horizontally split windows:
<pre>(setq truncate-partial-width-windows nil)</pre>
<strong><a name="wraps2"></a>Morsel 10 - Normal looking line wraps</strong>
<pre>M-x longlines-mode</pre>
or if you have it (Emacs 23+)
<pre>M-x global-visual-line-mode</pre>
Will toggle normal looking line wraps on and off.  If you want to get fancy, you can set up some default in your .emacs.d/init.el
<ol>
	<li>
<pre>;; Wrap lines visually</pre>
</li>
	<li>
<pre>(add-hook 'text-mode-hook 'longlines-mode)</pre>
</li>
	<li>
<pre>(setq longlines-wrap-follows-window-size 1)</pre>
</li>
</ol>
<strong><a name="backup"></a>Morsel 11 - Auto backup a little smarter</strong>

You'll soon notice Emacs scattering funny looking ~FILE and #FILE# backups across your directories. I like throwing all the auto backups into one directory and putting some sort of version number on them. This code is straight from the <a href="http://www.emacswiki.org/emacs/BackupDirectory">Emacs wiki</a>, it goes into you .emacs.d/init.el:
<ol>
	<li>
<pre>(setq</pre>
</li>
	<li>
<pre>     backup-by-copying t      ; don't clobber symlinks</pre>
</li>
	<li>
<pre>     backup-directory-alist</pre>
</li>
	<li>
<pre>     '(("." . "~/.saves"))    ; don't litter my fs tree</pre>
</li>
	<li>
<pre>     delete-old-versions t</pre>
</li>
	<li>
<pre>     kept-new-versions 6</pre>
</li>
	<li>
<pre>     kept-old-versions 2</pre>
</li>
	<li>
<pre>     version-control t)       ; use versioned backups</pre>
</li>
</ol>
<strong><a name="complete"></a>Morsel 12 - Autocomplete</strong>

This is quite useful, but you do have to install it. The installation instructions in the manual are clear. Take a look at <a href="http://www.emacswiki.org/emacs/AutoComplete">autocompletion for Emacs</a>.

<strong><a name="jump"></a>Morsel 13 - Jumping the line</strong>

C-n and C-p move your pointer up and down one line, but I can do this with my up and down arrow keys, so a redefined C-n and C-p to move up and down 5 lines at a time:
<ol>
	<li>
<pre>;; Move up and down five lines at a time</pre>
</li>
	<li>
<pre>(global-set-key "\C-n"</pre>
</li>
	<li>
<pre>    (lambda () (interactive) (next-line 5)))</pre>
</li>
	<li>
<pre>(global-set-key "\C-p"</pre>
</li>
	<li>
<pre>    (lambda () (interactive) (next-line -5)))</pre>
</li>
</ol>
<strong><a name="move"></a>Morsel 14 - Moving from one window to the other easilly</strong>

You split your window using C-x 2 and C-x 3 into as many pieces as you want. The default for moving to the next window is C-x O, but if you have 10 windows, this might take a while.

Here's how to use the arrow keys on your Num Pad to simply move up, down, left, or  right (up up down down left right...... nevermind) among your windows:
<ol>
	<li>
<pre>;; move to window to the left</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-4&gt;") 'windmove-left)</pre>
</li>
	<li>
<pre>;; move to window to the right</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-6&gt;") 'windmove-right)</pre>
</li>
	<li>
<pre>;; move to window below</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-8&gt;") 'windmove-up)</pre>
</li>
	<li>
<pre>;; move to window above</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-2&gt;") 'windmove-down)</pre>
</li>
</ol>
<strong><a name="delete"></a>Morsel 15 - Delete the entire word</strong>
This one's from a StackOverflow post that I cannot find right now. The kill-word function will delete a word from where your cursor is forward. What if you want to delete the entire word, including the part before your pointer?
<ol>
	<li>
<pre>;; kill entire word</pre>
</li>
	<li>
<pre>(defun my-kill-word ()</pre>
</li>
	<li>
<pre>  (interactive)</pre>
</li>
	<li>
<pre>  (backward-word)</pre>
</li>
	<li>
<pre>  (kill-word 1))</pre>
</li>
	<li>
<pre>(global-set-key (kbd "M-d") 'my-kill-word)</pre>
</li>
</ol>
<strong><a name="num"></a>Morsel 16 - Enabling the Num Pad</strong>

Depending how you're using Emacs. The keys for the num pad may not work the way you want. You can enable them to work like this:
<ol>
	<li>
<pre>;; Num pad enable</pre>
</li>
	<li>
<pre>;; The arithmetic operators already have keybindings,</pre>
</li>
	<li>
<pre>;; so you may not want to use those</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-1&gt;") "1")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-2&gt;") "2")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-3&gt;") "3")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-4&gt;") "4")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-5&gt;") "5")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-6&gt;") "6")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-7&gt;") "7")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-8&gt;") "8")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-9&gt;") "9")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-0&gt;") "0")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "M-O n") ".")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-enter&gt;") 'newline)</pre>
</li>
	<li>
<pre>;; Optional arithmetic operators</pre>
</li>
	<li>
<pre>;; These will change the regular F key defs too</pre>
</li>
	<li>
<pre>;; and you'll overide some macro and other settings</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;f2&gt;") "/")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;f3&gt;") "*")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;f4&gt;") "-")</pre>
</li>
	<li>
<pre>(global-set-key (kbd "&lt;kp-separator&gt;") "+")</pre>
</li>
</ol>
Of course, you have to make some choices sometimes. If you have the num pad enabled to show numbers and symbols, then you can't use it to move from one buffer to another. This is when a defining your own minor mode might come in handy.

<strong><a name="macros"></a>Morsel 17 - Making and storing macros</strong>

Define the macro. To start recording the macro:
<ol>
	<li>
<pre>C-x (</pre>
</li>
</ol>
Now type the keys, commands, etc you want done. This is just like in Excel.
Stop the macro recording with:
<ol>
	<li>
<pre>C-x )</pre>
</li>
</ol>
Now to save this macro we have to save it and insert it into our .emacs or init.el file.
Name the macro:
<ol>
	<li>
<pre>M-x name-last-kbd-macro</pre>
</li>
</ol>
Ok, now open up your .emacs or init.el file, and move your pointer (cursor) to where you want the code for your macro definition to go and type:
<ol>
	<li>
<pre>M-x insert-kbd-macro</pre>
</li>
</ol>
Now type in your <a href="http://netlumination.com/blog/three-steps-to-making-a-custom-keystroke-shortcut-in-emacs">custom keybinding</a>, something like:
<ol>
	<li>
<pre>(global-set-key (kbd "C-c n") 'my-macro)</pre>
</li>
</ol>
Of course, the keybinding (C-c n) and name (my-macro) will be your own.

<strong><a name="count"></a>Morsel 18 - Word Count</strong>
Emacs doesn't have a built in word count function. You can Lisp through a function, or you can avoid reinventing the wheel by calling the Unix word count function, "wc". Just remember that the "-w" option shows the actual word count. These lines of code in your .emacs or init.el file will define the function, "word-count" to count the words in the current file. I also set "C-c c" as the shortcut for this function:
<ol>
	<li>
<pre>;; Word count</pre>
</li>
	<li>
<pre>(defun word-count nil "Count words in buffer" (interactive)</pre>
</li>
	<li>
<pre>(shell-command-on-region (point-min) (point-max) "wc -w"))</pre>
</li>
	<li>
<pre>;; Shortcut for Word count</pre>
</li>
	<li>
<pre>(global-set-key (kbd "C-c c") 'word-count)</pre>
</li>
</ol>
Thanks to <a href="http://iquaid.org/2008/02/08/counting-words-in-emacs/">Karsten Wade and the discussion on this page</a>. There are many <a href="http://www.emacswiki.org/emacs/WordCount">word count alternatives in the Emacs Wiki</a>, and there's also a word-count-mode that you can download. I just like the code above for its simplicity if you're on a Unix like system anyway.
Have fun chewing on these eMACS!