---
layout: post
title: "Search and Replace with Regular Expressions"
date: 2014-09-16 17:06:36 -0600
comments: true
tags: emacs
---

I wrote the post that follows below so that I could remember how to use regular expressions for search and replace operations in Sublime Text. Since I just now made some headway in Emacs, I'll repost with some updates, again, primarily as a reference for myself.

There is no doubt that regular expressions are very powerful. I've found that the documentation for regular expressions is often as mysterious as the things that the documentation is supposed to explain. Keeping in mind that I am certainly no expert, learning even a little about the use of regular expressions can be quite valuable.

The normal search dialogue in text editors will find all uses of the search term. You might not want to find all uses of a term, but only those that match a certain pattern. For example, assume that I want to search for any dates in a long file. If the file contains many different dates, then searching successfully for each one would be tedious, if not impossible. If my dates are in the form "YYYY-MM-DD," then I can simply use the regular expression "dddd-dd-dd". The "d" finds a digit, so the search string locates every string of text that consists of four digits, followed by a hyphen, two digits, another hyphen, and ending with two digits.

It could be that I wasn't consistent in my dating scheme, some years have all four digits, and others have only two. The year could be first in some cases, but last in others. The search string "d&#42;-d&#42;-d&#42;" easily handles all of the variations. The asterisk is a repeat operator that matches the preceding character zero or more times. This search will find any three groups of digits separated by hyphens.

Search with regular expressions is powerful enough, but replacement is amazing. Any string contained in parentheses can be referenced in both search and replacement strings. That makes it simple to change just part of a string.

For example, imagine that I have a list of students that I copied from a database. Each line has the following format, "First Last", and I want to change it to "Last, First". The following regex search and replace accomplishes the task in one stroke:

<pre><code>
Search: ^(w*) (w*)n
Replace: $2, $1n
</code></pre>

This search finds every line consisting of just two words separated by a space. The <code>$1</code> refers to the string matched by the characters in the first set of parentheses, and <code>$2</code> refers to the string matched by the second set. The replacement string tells the editor to switch the words and insert a comma between them. This changes a list like this,

<pre><code>
George Washington  
John Adams  
Thomas Jefferson
</code></pre>

to

<pre><code>
Washington, George  
Adams, John  
Jefferson, Thomas
</code></pre>

Imagine how difficult it would be to do this with a long file by cutting and pasting each name! Regular expressions can use Boolean operators, wildcards, and different character types. Different languages have their own particular syntaxes for regular expressions, and I assume that text editors might also have different syntaxes. The examples all work in Sublime Text 2. It's well worth learning a little about how your preferred editor handles regular expressions, it can save a great deal of time and retyping.

The primary difference in Emacs is in referencing the strings to be searched for and used in the replace operation. The key is to put a backslash ("\") before the opening and closing parentheses in the search operation, and to use a backslash instead of a dollar sign in the replace operation. So, this will work for the preceding example:

<pre><code>
Search: ^\(\w+\) \(\w+\)
Replace: \2, \1
</code></pre>




