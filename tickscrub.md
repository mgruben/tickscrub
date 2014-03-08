tickscrub looks for a view file in the given directory, then drops a finalOutput file in that same directory.
####To create the view file:

**1.** Go to an event and "inspect element" within chromium on one of the listed ticket prices.

**2.** Scroll up until you see an element called &lt;tbody&gt;, and right-click that to "Copy as HTML."

**3.** Paste into a file named "view" in the directory of your choice (Directories should be named according to the convention event/dd_mm_yyyy_hhmm in 24-hour format).

**4.** Repeat 1-3 for as many pages as there are listings (until a better way can be found).
####Example usage:

The command ```$ tickscrub ~/events/basketball/globetrotters```
would look for ~/events/basketball/globetrotters/view, then through a combination of grep and sed
would output ~/events/basketball/globetrotters/finalOutput, which should be more human-readable.

Alternatively, the above could also be accomplished by
```$ cd ~/events/basketball/globetrotters``` followed by ```$ tickscrub .```
####Output Format
The columns, from left to right, would signify the following information:
```mysql
sectionName; ticketRow; quantity; deliveryMethod; q; wheelchair; parking; aisle; obstructed; piggyback;
```
Each line contains a complete entry with all of the above fields, and each field is separated by a ';'
####Troubleshooting
If there's no view file, tickscrub throws the following errors:

	bash: /finalOutput: Permission denied
	sed: can't read /view: No such file or directory
