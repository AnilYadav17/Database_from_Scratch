## IS NULL and IS NOT NULL

```sql
select * from employeebatch;
```

### _and_

```sql
select * from employeebatch where city=null;
```

<br>

### **_Note_**

**NULL Means there is no value is known u or value has not been provided. It is not the same as the following: <br>
0 <br> '' <br> 'Null' <br> false**

**_Is null is used to find rows where a column contains null._**

```sql
select * from employeebatch where city is null;
```

```sql
select * from employeebatch where city is not null;
```

<br>

### **_IS NULL with AND_**

```sql
select * from employee where city is null and salary > 35000;
```

<br>

### **_Operator presedence with AND ,OR and NOT_**

When we use multiple conditions inside where mysql has to decide which conditions to evaluate first.

```sql
select * from employeebatch where city="Indore" or city="Bhopal" and salary>50000;
```

In mySql the presedence is
<br>1. NOT <br>2.AND <br>3.OR
<br>
<br>
When we write :

```sql
where a or b and c;
becomes
where a and (b and c);
```

so our query becomes ->

```sql
select * from employeebatch where city="Indore" or (city="Bhopal" and salary>50000);
```

<br>

**_Write a query to fetch employees who are from indore or bhopal, and there salary must be greater than 40000_**

```sql
select * from employeebatch where (city="Indore" or city="Bhopal") and salary>40000;
```

**_Write a query whose city is not indore_**

```sql
select * from employeebatch where not city="Indore";
```

**_Equivalent to_**

```sql
select * from employeebatch where not city<>"Indore";
```

**_Write a query to give me employees who are neither from INDORE nor BHOPAL._**

```sql
select * from employeebatch where not (city="Indore"  or city="Bhopal");
```

<br>

### NOT with AND

**_Write a query to give me employees who are not from Indore,Bhopal and earning more than 50000_**

```sql
select * from employeebatch where not (city="Indore"  or city="Bhopal") and salary > 50000 ;
```

<br>

```sql
select * from employeebatch where city="Indore" or city="Bhopal" and salary>40000 and age>35;
```

**_This query is converted into:_**

```sql
select * from employeebatch where city="Indore" or (city="Bhopal" and salary>40000 and age>25);
```

<br>

**_Write a query to give me employees who are from Indore,Bhopal and earning more than 40000 and age greater 25_.**

```sql
select * from employeebatch where (city="Indore" or city="Bhopal") and (salary>40000 and age>25);
```

<br>

So,

```sql
where not a or b and c
becomes
where (not a) or (b and c)
```

<br>
