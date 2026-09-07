## FOREIGN KEY

A combination of a combination of a column in one table that references in a candidate key normally a primary key or unique key in another table.

Its main perpose to maintain refferential integrity between related tables.

|Did|dname|
|---|---|
|1|IT
|2|HR
|3|IT

and

|empid|empname|deptid|
|---|---|---|
|101|Anil|1
|102|Harsh|2


want to insert,<br>
104 , Abhi, 10 <br>
The following query than it will give error because department10 exist.
<br>

---
### PARENT TABLE AND CHILD TABLE
PARENT TABLE - The table containing the refferenced key.
Here Depatment table is referenced table.

CHILD TABLE (OWNER) - Table containing the foreign key is called child table,(Employee Table).

---
---
***EXAMPLE2 ->  CUSTOMER and ORDERS***

|Cid|Cname|email|
|---|---|---|
|101|Anil|
|102|Dipu|
|103|Rashmika|

|Oid|Odate|Amount|CustID|
|---|---|---|---|
|1|2026-09-07|499|101
|2|2026-09-08|499|101
|3|2026-09-09|999|103

Oid -> Primary Key and CustId -> Foriegn Key

---
---
***EXAMPLE3 ->  DOCTOR ,PATIENT and APPOINTMENT***
|Did|Dname|Spec|Add|
|---|---|---|---|
|101|Anil|

<br>

|Pid|Pname|Disease|Add|
|---|---|---|---|
|1|Abhi|

<br>

|Aid|Did|Pid|Date|
|---|---|---|---|
|201|101|1|2026-09-07

