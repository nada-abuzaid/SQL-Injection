# SQL-injection

<img src="https://miro.medium.com/max/1332/1*QQJPSw8vXNjdAiWPVa74Lg.png" />

## Bad Practice

- Poor Normalization
- Composite Primary Keys
- Using `SELECT *`
- Using `WHILE(1=1)` or `WHILE(""="")`
- Using batched SQL statements

### Poor Normalization

Database Normalization is the process of organizing the fields and tables in a relational database in order to reduce any unnecessary redundancy.
The process usually involves breaking down larger tables (many columns) into smaller more manageable tables and relating the two using primary keys and foreign keys. It usually follows common logic.

<img src= "https://bs-uploads.toptal.io/blackfish-uploads/uploaded_file/file/191035/image-1582221259279-2f1ab5023099241f071fd10726b0511d.png" />

### Composite Primary Keys

Many database designers talk nowadays about using an integer ID auto-generated field as the primary key instead of a composite one defined by the combination of two or more fields. This is currently defined as the “best practice” and, personally, I tend to agree with it.

<img src ="https://bs-uploads.toptal.io/blackfish-uploads/uploaded_file/file/191036/image-1582221333714-d003c063c7d927fb3c6193be1798f162.png" />

### Using `SELECT *`

- Unneccessary I/O
- Increased Network traffic
- More Application memory
- Risky while copying data

### Using `WHILE(1=1)` or `WHILE(""="")`

<img src="https://miro.medium.com/max/504/1*ibLcqnPa3NrXQeETn5GDNg.png" />

```JS
studentId = getRequestString('StudentId');
sqlQuery = 'SELECT * FROM Students WHERE StudentId = ' + studentId;
```

Look at the example above. The original purpose of the code was to create an SQL statement to select a student, with a given student id.

If there is nothing to prevent a user from entering "wrong" input, the user can enter some "smart" input like this:

<img src="https://e.top4top.io/p_225783i3d1.png" />


Then, the SQL statement will look like this:

```sql
SELECT * FROM students WHERE StudentId = 120 OR 1=1;
```

The SQL above is valid and will return ALL rows from the "Users" table, since OR 1=1 is always TRUE.

A hacker might get access to all the user names and passwords in a database, by simply inserting 120 OR 1=1 into the input field.

### Using batched SQL statements

A batch of SQL statements is a group of two or more SQL statements, separated by semicolons.

The SQL statement below will return all rows from the "Students" table, then delete the "Mentors" table.

```sql
 SELECT * FROM Students; DROP TABLE Mentors 
 ```
Look at the following example: 

 ```JS
studentId = getRequestString('StudentId');
sqlQuery = 'SELECT * FROM Students WHERE StudentId = ' + studentId;
```
And the following input:

<img src="https://c.top4top.io/p_2257e0dzr1.png" />

The valid SQL statement would look like this:
```sql
SELECT * FROM Students WHERE StudentId = 120; Drop Table Mentors;
```
