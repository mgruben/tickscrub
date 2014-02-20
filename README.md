tickscrub
=========

Reads ticket pricing information and updates a corresponding MariaDB logging database.

In general, the steps involved are:

(1) obtaining as HTML-source the raw ticketing information.  This information will likely be unformatted for human readability, and will likely also contain information which is irrelevant for the logging database.

(2) trimming the HTML-source so that only relevant information remains, perhaps also with some basic formatting tags that ease the later parsing of the information.

(3) parsing the trimmed source.  This will probably occur through some object-oriented programming language like Java due to its presumed superiority for such tasks.

(4) logging to and updating the MariaDB database.  For example, on the first run of tickscrub, the database will be empty, and all information parsed from the trimmed source will need to be added to the database.  On subsequent runs of tickscrub, the database will already be at least partially (and possibly fully) populated with unique tickets, but will need those tickets to be updated with the current pricing information at the time of the scrub, will need to make additional entries for new unique tickets (those which haven't been seen before), and will need to keep unique ticket entries which no longer exist (who knows, they may pop up again in subsequent scrubs).
