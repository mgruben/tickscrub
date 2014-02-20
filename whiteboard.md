(How to generate ticket IDs? How to add new ticket IDs when new (yet-unseen) tickets go on sale?)
--for each finalOutput paragraph (probably want to use Java or some other object-oriented language to read the text paragraphs and parse into variables):
(1) read Section Name and Ticket Row,
(2) check if that unique combination is already present in table 2 (if not, append it as the next TicketID in table 1 and table 2 (along with row and section) and table 3 (along with flavors)),
(3) read from table 2 the ticket ID of that unique row+section combination,
(4) add price data to table1 for that ticket ID (in column named for the time the data was collected)
--asked contributor to implement Java parsing of the finalOutput file:
"For reference, the variables that need to be read (and probably stored in memory, unless we want to get fancy with conditional reads) are:
(1) sectionName, (2) ticketRow, (3) price("q"), (4) deliveryMethod, (5) IsWheelchair("wheelchair"), (6) IsAisle("aisle"), (7) IsParking("parking"), (8) ticketQty[, then (9) ticket ID from the database; a necessary crutch variable to be able to reference the same ticket across multiple SQL tables]"
--You'll probably need to provide the SQL query and table-modification calls for him to implement.
