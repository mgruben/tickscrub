##Java/MariaDB Whiteboard
--for each finalOutput paragraph (probably want to use Java or some other object-oriented language to read the text paragraphs and parse into variables):

**(1) read Section Name and Ticket Row from finalOutput**

```That's all you Java man```

**(2) check if that unique combination is already present in the 'row_and_section' table of the event database**

```select ticket_id from row_and_section where section_name="[some section]" and ticket_row="[some row]"```
(Note, the above isn't really a boolean test.  It actually returns that combo's ticket_id (or not, if the combo doesn't exist).  Will want to figure out how to return TRUE/FALSE for this step.

Example of step (2):
```mysql
MariaDB [tick_db]> select * from row_and_section;
+------------------------+------------+-----------+
| section_name           | ticket_row | ticket_id |
+------------------------+------------+-----------+
| Floor 108              | BB         |         1 |
| Lower Level Center 119 | P          |         2 |
+------------------------+------------+-----------+
2 rows in set (0.00 sec)

MariaDB [tick_db]> select ticket_id from row_and_section where section_name="Floor 108" and ticket_row="AB";
Empty set (0.01 sec)

MariaDB [tick_db]> select ticket_id from row_and_section where section_name="Floor 108" and ticket_row="BB";
+-----------+
| ticket_id |
+-----------+
|         1 |
+-----------+
1 row in set (0.00 sec)
```
###If Entry Doesn't Exist
If MariaDB returns an empty set ```no idea how to tell this yet``` the ticket doesn't exist, and we'll have to create an entry.

To do this, we'll, for example:
```mysql
insert into row_and_section (section_name, ticket_row) values ("Lower Level Center 119", "P");
insert into price_over_time (02_18_2014_2040) values (475.25);
insert into ticket_features (delivery_method, qty) values ("UPS", "1-4");
```
Note: If there are **special features**, they must be specified as follows (If there aren't, don't worry about specifying them.  It's unclear whether we know for certain that a given ticket DOESN'T have a feature simply because it's not identified
```mysql
insert into ticket_features (IsAisle, IsWheelchair, IsParking, delivery_method, qty) values (1, 1, 1, "Electronic", "2");
```
###If Entry Already Exists
**(a) read from table 'row_and_section' the ticket ID of that unique row+section combination**
```select ticket_id from row_and_section where section_name="[some section]" and ticket_row="[some row]"```

**(b) add price data to table 'price_over_time' for that ticket ID (in column named for the time the data was collected)**

Generally, this will be done by issuing a command similar to
```mysql
update price_over_time set 02_18_2014_1936 = 450 where ticket_id = 1;
```
This command results in the following database change:
```mysql
MariaDB [tick_db]> select * from price_over_time;
+-----------+-----------------+-----------------+
| ticket_id | 02_18_2014_1936 | 02_18_2014_2040 |
+-----------+-----------------+-----------------+
|         1 |            NULL |          475.00 |
|         2 |            NULL |          475.25 |
+-----------+-----------------+-----------------+
2 rows in set (0.00 sec)

MariaDB [tick_db]> update price_over_time set 02_18_2014_1936 = 450 where ticket_id = 1;
Query OK, 1 row affected (0.46 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [tick_db]> select * from price_over_time;
+-----------+-----------------+-----------------+
| ticket_id | 02_18_2014_1936 | 02_18_2014_2040 |
+-----------+-----------------+-----------------+
|         1 |          450.00 |          475.00 |
|         2 |            NULL |          475.25 |
+-----------+-----------------+-----------------+
2 rows in set (0.00 sec)

```
Also, multiple columns (data pulls) can be entered at one time, as shown in the below example continuing the previous one:
```mysql
MariaDB [tick_db]> update price_over_time set 02_18_2014_1936 = 666, 02_18_2014_2040 = 667 where ticket_id = 2;
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [tick_db]> select * from price_over_time;
+-----------+-----------------+-----------------+
| ticket_id | 02_18_2014_1936 | 02_18_2014_2040 |
+-----------+-----------------+-----------------+
|         1 |          450.00 |          475.00 |
|         2 |          666.00 |          667.00 |
+-----------+-----------------+-----------------+
2 rows in set (0.00 sec)

```

For reference, the variables that need to be read (and probably stored in memory, unless we want to get fancy with conditional reads) are:

(1) sectionName, (2) ticketRow, (3) price("q"), (4) deliveryMethod, (5) IsWheelchair("wheelchair"), (6) IsAisle("aisle"), (7) IsParking("parking"), (8) ticketQty[, then (9) ticket ID from the database; a necessary crutch variable to be able to reference the same ticket across multiple SQL tables]"

####Remaining unresolved issues:
* How to make sure Ticket IDs align as data is added to the database?
  * (1) We add each ticket object to 3 tables in a row
    * Currently, Ticket IDs are 'auto_increment'ed for each of our three tables independenty
    * I'm worried that we lose efficiency this way, and that if anything gets off our DB is misaligned, though in theory it should always work perfectly.
  * (2) We add row and section information for all tickets first, then go back through the database and update the Java memory of stored tickets with whatever Ticket ID the database assigned, then add pricing information and features to their respective tables w/ Ticket ID manually.
    * This way lessens the risk that our database gets mis-aligned, since we're double checking Ticket ID before we dump information in
    * This approach is perhaps more computationally- or memory-intensive, but creating entries for an entire table is simplified to a single command

####Solved issues
* How to generate ticket IDs?
  * Ticket IDs are generated automatically through use of the "auto_increment" option.  Thus the table 'row_and_section' appears as follows:
```mysql
MariaDB [tick_db]> describe row_and_section;
+--------------+----------------------+------+-----+---------+----------------+
| Field        | Type                 | Null | Key | Default | Extra          |
+--------------+----------------------+------+-----+---------+----------------+
| section_name | varchar(100)         | NO   |     | NULL    |                |
| ticket_row   | varchar(10)          | NO   |     | NULL    |                |
| ticket_id    | smallint(5) unsigned | NO   | PRI | NULL    | auto_increment |
+--------------+----------------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)
```
