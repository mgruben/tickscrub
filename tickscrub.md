# tickscrub looks for a view file in the given directory, then drops a finalOutput file in that same directory.
# To create the view file, go to an event and "inspect element" within chromium on one of the listed ticket prices.
# Scroll up until you see an element called <tbody>, and right-click that to "Copy as HTML."
# Then, paste into a file named "view" in the directory of your choice.
# You'll probably have to do this for as many pages as there are listings until a better way can be found.
# Directories should be named according to the convention event/dd-mm-yyyy_hhmm in 24-hour format.
tickscrub() {
	sed -e 's/.span class/\n&/g' -e 's/.tr class/\n&/g' $1/view | grep 'sectionNa\|ticketRow\|ticketQt\|deliveryMet\|\"q\"\|aisle\|parking\|wheelchair' | sed '/\$/ a\ ' > $1/finalOutput
}