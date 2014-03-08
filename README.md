tickscrub
=========

Reads ticket pricing information and updates a corresponding MariaDB logging database.

In general, the steps involved are:

(1) obtaining as HTML-source the raw ticketing information.  This information will likely be unformatted for human readability, and will likely also contain information which is irrelevant for the logging database.

(2) trimming the HTML-source so that only relevant information remains, perhaps also with some basic formatting tags that ease the later parsing of the information.

(3) parsing the trimmed source.  This can likely occur a variety of ways, but at present is accomplished through a variety of ```sed```, ```grep```, and ```awk``` commands and their relatives.

(4) logging to the MariaDB database.

It would be nice if we could identify individual unique tickets from the present information, but unfortunately that is not possible at present.  Could we _guess_ that a ticket with x,y,z,a identifiers is the same as another with x,y,z,a when those are the only ones with x,y,z,a?  Sure, but it wouldn't always be right, and we would have no way of knowing when we were guessing incorrectly.
