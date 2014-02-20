Examples contained in this folder will, at least initially, be of the
following format:
###"view" files
These are raw HTML dumps, and may contain a return character or two
(because leafpad doesn't like it when you paste a lot of text without
a return).  This as source-y as it's going to get.
###"finalOutput" files
These are view files which have been passed through the tickscrub script.
They've been (mostly) cleaned of irrelevant information, and have also
been formatted for basic human readability (i.e. each span starts on a new
line and each ticket 'object' is separated by two return characters.
Visual grouping is great, and maybe it helps an html-parser, but at present
these files are in a format that can't be easily stuffed into a MariaDB file.
