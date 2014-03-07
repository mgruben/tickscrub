##Java/MariaDB Whiteboard
--for each finalOutput paragraph (probably want to use Java or some other object-oriented language to read the text paragraphs and parse into variables):

**(1) read from finalOutput:**
* Section Name ("section")
* Ticket Row ("row")
* Ticket Price ("price")
* Delivery Method ("delivery")
* Whether Ticket is Wheelchair-accessible ("isWheelchair")
* Whether Ticket is an Aisle Seat ("isAisle")
* Whether Ticket includes Parking ("isParking")
* The Number of Tickets for Sale ("quantity")

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

For reference, the variables that need to be read (and probably stored in memory, unless we want to get fancy with conditional reads) are:

(1) sectionName, (2) ticketRow, (3) price("q"), (4) deliveryMethod, (5) IsWheelchair("wheelchair"), (6) IsAisle("aisle"), (7) IsParking("parking"), (8) ticketQty[, then (9) ticket ID from the database; a necessary crutch variable to be able to reference the same ticket across multiple SQL tables]"

####Remaining unresolved issues:
None [that I'm writing here]!  Huzzah!
####Solved issues
* How to generate ticket IDs?
  * Ticket IDs are generated automatically through use of the "auto_increment" option.
  * Ticket IDs are also probably almost entirely irrelevant for our purposes.
