---
layout: post
title: Stringp, Nil Error in Emacs
tags:
- emacs 
comments: true
date: 2015-06-04 20:52:54 -0500
---
This is one of those posts that serve only to remind me of something in the future. My Emacs configuration was working well on one machine.  Whenever I opened dired on another machine, though, this error was returned:

`wrong type argument: stringp, nil`

Finally, I remembered that I had required GNU ls in my Emacs settings, and had not installed it on the machine in question. A quick "brew install coreutils" to install the GNU Command Line Tools with Homebrew did the trick.
