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
'/path/to/finalOutput'
into TABLE poll_mm_dd_yyyy_hhmm
COLUMNS TERMINATED BY ',' ENCLOSED BY '"'
LINES TERMINATED BY '\n';
```
or some similar command which actually works.  The above has a nasty habit of including the next column name along with the field's value itself, such that the entry for ```sectionName``` is ```Lower Level Baseline 124; "ticketRow"``` where it should end at the semicolon to instead read ```Lower Level Baseline 124```

####Remaining unresolved issues:
None [that I'm writing here]!  Huzzah!
####Solved issues
* How to generate ticket IDs?
  * Ticket IDs are generated automatically through use of the "auto_increment" option.
  * Ticket IDs are also probably almost entirely irrelevant for our purposes.
