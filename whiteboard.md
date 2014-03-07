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

**(2a) Create (Horizontal->Vertical) Entry in Database**

To do this, we'll, for example:
```mysql
insert into poll_03_06_2014_1903 (section, row, price, delivery, isWheelchair, quantity) values ("Lower Level Center 119", "P", 475.25, "Electronic", 1, "2-4");
```
And will iterate through each paragraph.

Note: ```isWheelchair```, ```isAisle```, and ```isParking``` don't have to be specified since their values default to NULL (~unknown) when not specified.

**(2b) Create (Vertical->Horizontal) Entry in Database**
To do this, we'll, for example:
```mysql

```

For reference, the variables that need to be read (and probably stored in memory, unless we want to get fancy with conditional reads) are:

(1) sectionName, (2) ticketRow, (3) price("q"), (4) deliveryMethod, (5) IsWheelchair("wheelchair"), (6) IsAisle("aisle"), (7) IsParking("parking"), (8) ticketQty[, then (9) ticket ID from the database; a necessary crutch variable to be able to reference the same ticket across multiple SQL tables]"

####Remaining unresolved issues:
None [that I'm writing here]!  Huzzah!
####Solved issues
* How to generate ticket IDs?
  * Ticket IDs are generated automatically through use of the "auto_increment" option.
