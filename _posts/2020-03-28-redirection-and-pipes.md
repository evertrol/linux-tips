---
layout: post
title: Redirection and pipes
---

In Linux, you can send the output of a command easily to a text file. Or, vice versa, the contents of a (text) file as input to a command. The term for this is rediction: you redirect the contents of something somewhere else. Linux (or rather, the shell) uses the `>` and `<` operators for this: the first one sends the output of a command on the left side to a file on the right, the second reads the contents of a file on the the right, and sends it to the command on the left.

An example would be `ls > listing.txt`, where the file `listing.txt` will contain the listing of files in the current directory. The other way around, with `<`, is less common. It can be useful if you have a command that asks a series of questions, and you already have the answers in a text file (one answer per line). Then `ask < answers.txt` will work nicely.

The output is generally called standard output, or `stdout` (think of standard as default, or normal). Standard input (`stdin`) is the opposite, but there is also standard error, `stderr`. (There is no "standard input error": that would mean you're telling the computer it's wrong. That may happen, but that's usually a different wrong than what is meant here.) `stderr` is for error messages. Usually, these are also written in the terminal, but this doesn't have to be the case. More importantly, it means error messages and normal output can be separated! So if `ls` above encounters an error, you would still see that, even if you redirect `stdout`. For example, `ls non-existent-directory > listing.txt` will show the error "ls: non-existent-directory: No such file or directory" in the terminal. Note that `listing.txt` will still exist, but it's empty. 

If you also would like to send stderr to a file, you can do that: `ls non-existent-directory > listing.txt 2> errors.txt`. The `2` indicates `stderr`: `stdout` is `1`, but that's the default. There is a problem if you want to write both `stdout` and `stderr` to the same file: the outputs will overwrite the previous file, and you only will get one (which one depends on which stream, `stdout` or `stderr`, was the last to be created). The trick is to send `stderr` to the same stream as `stdout`, and send the latter to a file: `ls non-existent-directory 1> listing.txt 2>&1`. Perhaps confusingly so, the order of the two redirects does matter.

It is important to keep in mind that each time you run a command with redirection, the existing output file is overwritten. If you want to *append* to a file, use `>>` instead. This works with `stdout` and `stderr`, for example, `ls non-existent-directory 1>> listing.txt 2>> errors.txt`. When redirection `stderr` to `stdout`, this is of course not needed, just for files.

Examples for `<` will be for another post, with some fancier use of `cat`.

## Pipes

Closely related to redirection streams are pipes, with the pipe operator `|` (the character name is sometimes also called "pipe", though "vertical bar" is probably clearer. I often call certain characters by their function, e.g., `-` can be minus, dash or option, depending on its usage). While redirects send output to (or read input from) passive files, pipes send output of one program to another program that is actively reading input, line by line. This is incredibly powerful, since it allows you to chain various commands to get a result, whereby each command does just one thing. In another post, I've already showed `du -h | sort -h`, but if the output is long and you want to see everything without scrolling up (if the terminal even allows that), you can do `du -h | sort -h | more`.

To be clear, `ls | listing.txt` does not work: a file is something passive (and it probably doesn't even exist yet), while a pipe needs two active commands on either side. Neither will `du -h > sort -h` work: you will get a file `sort` instead, and the second `-h` is interpreted as a (superfluous) option to `du`.


## /dev/null and other special devices

Sometimes, you want to run a command, but ignore all its output. You can redirect this to the special file `/dev/null`, which simply absorbs everything (`/dev/blackhole` would also be a good name, albeit less computer science technical). Avoid doing this for `stderr` though: errors are important to notice!

Other special devices are `/dev/stdout`, `/dev/stdin` and `/dev/stderr`, which are the representations in the file system of `stdout`, `stdin` and `stderr`. If you redirect your `stdout` to `/dev/stdout`, it will just print to the terminal!
