---
layout: post
title: text editors
---

For a lot of things, you will be editing text files. Most of the times, these are configuration files or simple data files. The latter could be a very simple, line by line file, that is, just plain text (which is also data), or a more strictly formatted text file, such as comma-separated values (CSV) or JavaScript-Object-Notation (JSON). These latter two types are still text files (you can open them with a text editor), but they are formatted in a way that makes it easier to transfer data between programs.

I recommend terminal-only text editors. These can be a bit confusing, annoying even, to work with at first, since you can't use the mouse: everything is done using the keyboards, often as special key-combinations, such as `control-q` (`^q`, where `^` is short for the control key) to quit an editor.

One of the oldest, most infamous text editor, is VI, or nowadays VIM (VI improved). VI uses two modes: a command mode mode to move around or perform operations on pieces of text, and an insertion mode to enter text. This can be very confusing at first, and the keyboard keys (commands) to switch between them, and in general work with VI, also don't appear natural. This is in a large part due to VI's (long) history. But, VI will be installed on almost any system, and knowing the basics can be useful. You start VI by typing `vi` on the command line in a terminal, which immediately introduces one of the biggest problems in VI: how to exit VI? Always first press escape, that will guarantee you are in command mode. Then, to save the current file and exit, press `ZZ` (twice `shift-z`), or to not save the file and exit, type `:q!` followed by enter. Other than these commands, I will not explore VI further: there are plenty of introductions on the internet to read.

Emacs is another famous text editor. Perhaps slightly easier than VI in its use (it does not have a separate command mode: you can just move around as you would expect with the arrow keys), it still has some awkward key commands. Although some of these commands have been incorporated by various shells as a default to edit commands on the command line (more in another tip). To start emacs, use `emacs`. To exit emacs, use `^x ^c`.

Two simpler editors, very useful for quickly editing configuration files, are Pico (`pico`) and Nano (`nano`). They are very similar, so check which one is installed and try it out. Most editing commands use `control-` with some letter, and the most common are listed at the bottom. To exit, use `^x`.

Finally, there are more graphical editors, such as `gedit` and `kate`. You can use these, but these may not be available on remote systems that don't have a graphical user interface and that you can only use access through a terminal via, for example, `ssh`. Web servers and single board computers (e.g. Raspberry PI) come to mind.

Some of the above listed editors may not be installed. Installation can be done through the package manager for your system, or directly on the command line: `sudo apt install emacs-nox`, `sudo apt install nano` or `sudo apt install pico` would do this; you'll be asked for your admin password: if you enter that, you won't get any feedback in the form of asterisks, so don't be surprised! (Note on `emacs-nox`: emacs has a graphical variant: `emacs-nox` is the terminal-only variant, which doesn't require various graphical libraries. In particular if you are on machine with no graphical framework but want to install Emacs (as I sometimes do), install `emacs-nox`.)
