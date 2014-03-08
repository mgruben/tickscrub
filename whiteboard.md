##Java/MariaDB Whiteboard
--for each finalOutput paragraph (probably want to use Java or some other object-oriented language to read the text paragraphs and parse into variables):

**(1) read from finalOutput:**
* Section Name ("sectionName")
* Ticket Row ("ticketRow")
* The Number of Tickets for Sale ("quantity")
* Delivery Method ("deliveryMethod")
* Ticket Price ("q")
* Whether Ticket is Wheelchair-accessible ("wheelchair")
* Whether Ticket includes Parking ("parking")
* Whether Ticket is an Aisle Seat ("aisle")
* Whether Ticket features an Obstructed View ("obstructed")
* Whether Ticket is for a 'piggyback' seat ("piggyback")

**(2) Create (Horizontal->Vertical) Entry in Database**

Note that this is probably most easily accomplished through the issuance of
```mysql
LOAD DATA LOCAL INFILE
'/path/to/event/date/finalOutput'
into TABLE poll_mm_dd_yyyy_hhmm
FIELDS TERMINATED BY ';'
LINES TERMINATED BY '\n'
```
The above code currently works.  Maybe it won't always, and bug tracking is a never-ending quest for perfection, but currently it works for our purposes.

Additional useful commands for playing around in, _inter alia_, MySQL Workbench are as follows:
```mysql
SELECT * FROM poll_mm_dd_yyyy_hhmm
```
This command returns all entries from the specified table
```mysql
DELETE FROM poll_mm_dd_yyyy_hhmm
```
This command DELETES all entries from the specified table.  You'll want to be careful to only issue this command when you really, really mean to (though with data redundancy, issuing it inadvertently would be more of an annoyance than a catastrophe).


####Remaining unresolved issues:
None [that I know of]!  Huzzah!
####Solved issues
* How to generate ticket IDs?
* How to slay the Gorgon
* How to win friends and influence people
* How tie a tie (google autocomplete suggestion)
* How to boil eggs (another google autocomplete suggestion)
