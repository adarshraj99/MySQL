SQL is a schema(collection of different datas) object. It is used by the server to speedup the data retrival by using pointer. It can reduce dick I/O operation time by using a rapid path access method.
eg: In an employee table with EmployeeID as Primary Key, all other data used is sorted by EmployeeID and physically stored in a tree like structure: 
![image](https://github.com/adarshraj99/MySQL/assets/122180050/0e6d1377-7d89-4ed1-8902-a9a010d2c463)
![image](https://github.com/adarshraj99/MySQL/assets/122180050/3438ee0c-d87c-4063-aa19-38bd64202539)
In the tree like structure bottom one is called Data pages or leaf Nodes(contain employee data rows). 
Top one is called Root node and all the intermidiate ones are called Intermidiate rows. root node and intermidiate rows have primary keys eg:EmployeeID and have a pointers to reach to the correct data. 

Data are arranged by compiler in diffrent ranges in different intermidiate rows to saperate the data pages and to create pointers. see below: 
![image](https://github.com/adarshraj99/MySQL/assets/122180050/b7089962-57f7-49ad-a008-fe39f4e7b787)
Here, in 3 steps only SQL server found the needed data because of **data clustring** and tree structure. First with clustered data on number ranges in imtermediate rows ,then with EmployeeID in the Data Pages. 
In real code term: Create table ,then create columns ,create column datas: 
![image](https://github.com/adarshraj99/MySQL/assets/122180050/005cf57e-4a75-4dc9-b62f-8ba2dbe957ac)

If need to find any table data by a non-primary Key. SQL need to iterate over lots of data one by one and may timeout. Number of rows read can be read by 'Clustered Index scan' module in SQL server managememt studio tool. Alternatively, **non-clustered** Index can be created on the searched column name(non-primary key). eg : 
Creating index on non-clustered data In Employees table in Name Column in EmployeedDB.  

![image](https://github.com/adarshraj99/MySQL/assets/122180050/80a9efef-7e34-44af-95e8-099881cd8135)

In non-clustered index we don't have Primary key. we have row_locators and Key_value pairs. The non-primary key is sorted alphabetically and assigned their row primary keys by compiler. eg: If we are searching by non-primary key name then name is sorted and assigned the primary key EmployeeID. Then, compiler searches with sorted name like a dictionary search(book dictionary) then switches to clustered data table and gets other datas.

Image of Un-clustered data table: 
![image](https://github.com/adarshraj99/MySQL/assets/122180050/6c935c1b-1e35-40da-a9de-4ce93cfedd1b)
