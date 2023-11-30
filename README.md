# MySQL_Matlab
How to configure MySQL in Matlab for timetable storing From MATLAB. 
# MySQL Workbench
Download and install MySQL Server from below link

[https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/)

At stage of installation " Run MySQL Configurator " to configure MySQL Server.
If it is showing that the port 3308 alredy in used. Please stope the server of MySQL80 from windows services.
Give the password as you like. 
Execute and Finish the MySQL Server installation
# MySQL Workbench
Download MySQL Workbench from  below link

https://dev.mysql.com/downloads/workbench/

Download the recent version and install it.

Run th MySQL Workbench 

Click Home icon at top of MySQL Workbench
MySQL Connections will Open
Click on + icon for setup new connection. Give the connection name as you like (I am giving matpdcdb)
Connection method: Standard(TCP/IP)
Hostname:127.0.0.1
Port: 3306
user:root
* click on test connection
* it will ask for password. Give the password
* It will show message with successfully made the MySQL connection.
* then click on Ok on setup connection window
* A new MySQL Connection will appear.
* Now click on it and give password connection will open.
* In navigator panel click on bottom Schemas. Then click on anywhere on Navigator panel. it will show option to create new schema.
* Create new schema with the name you like( I am giving matpdcdb) and clik apply then on new window again click apply and finish.
* In left Navigator panel new schema with matpscdb name will be appear.
* Now close it
  # ODBC Driver
  > Download the ODBC driver from the below link
* https://downloads.mysql.com/archives/c-odbc/
* Download the 64 bit drivers and install them
  # Matlab Configuration
* Open the matlab and open database explorer from APP tab.
* Click on Configure Database Source
* click on Configure ODBC data Source
* Click on System DNS tab
* Click on Add
* Click on MySQL ODBC ANSI Driver
* Click ok
* new window will open
* Give the Datasourse name- matpdcdb (Your database name)
* TCP/IP Server: localhost
* Give the username: root
* password- previous database password (root in my case)
* Click on Database from dropdown arrow: matpdc (in my case, I made this in  MySQL Workbench as schema)
* click ok
* and again ok
* close the data exlorer window.
* Write below code in Matlab and run it

  conn==database('matpdcdb', 'root','root')

> This will show following output
conn= 

  connection with properties:

                  DataSource: 'matpdcdb'
                    UserName: 'root'
                     Message: ''
                        Type: 'ODBC Connection Object'
  Database Properties:

                  AutoCommit: 'on'
                    ReadOnly: 'off'
                LoginTimeout: 0
      MaxDatabaseConnections: 0

  Catalog and Schema Information:

              DefaultCatalog: 'matpdcdb'
                    Catalogs: {'information_schema', 'matpdc', 'matpdc_db' ... and 6 more}
                     Schemas: {}

  Database and Driver Information:

         DatabaseProductName: 'MySQL'
      DatabaseProductVersion: '8.0.34'
                  DriverName: 'myodbc8a.dll'
               DriverVersion: '08.00.0033'

> Now write beow command to write to database
tablename=My_Database_Table (If table name is not present it will create the table with this name)
sqlwrite(conn,tablename,Data) ( Where Data is the table you wan t to write to database)
* Below is the Data
data =
```matlab
  3×3 table

         PMU_time             Var1       Var2 
    ___________________    __________    _____

    2023-11-13 09:53:51    1.6999e+09    0.767
    2023-11-13 09:53:51    1.6999e+09    0.775
    2023-11-13 09:53:51    1.6999e+09    0.783
```matlab

# MySQL_Matlab

This repository provides instructions and code for configuring MySQL in MATLAB to store timetables. Follow the steps below to set up MySQL in MATLAB, including installing MySQL Server, MySQL Workbench, ODBC Driver, and configuring MATLAB for database connection.

## MySQL Server Installation

1. Download and install MySQL Server from [https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/).
2. During installation, run MySQL Configurator to configure MySQL Server.
3. If the port 3308 is already in use, stop the MySQL80 server from Windows services.
4. Set a password of your choice during installation.
5. Complete the MySQL Server installation.

## MySQL Workbench Installation

1. Download MySQL Workbench from [https://dev.mysql.com/downloads/workbench/](https://dev.mysql.com/downloads/workbench/).
2. Install the latest version of MySQL Workbench.
3. Run MySQL Workbench and click on the Home icon at the top.
4. Open MySQL Connections and set up a new connection.
5. Connection details:
   - Connection Name: Choose a name (e.g., matpdcdb).
   - Connection Method: Standard(TCP/IP)
   - Hostname: 127.0.0.1
   - Port: 3306
   - User: root
6. Test the connection by providing the password.
7. Once successful, click OK to set up the connection.
8. Create a new schema (database) in the Navigator panel.
9. Close MySQL Workbench.

## ODBC Driver Installation

1. Download the ODBC driver from [https://downloads.mysql.com/archives/c-odbc/](https://downloads.mysql.com/archives/c-odbc/).
2. Download and install the 64-bit drivers.

## MATLAB Configuration

1. Open MATLAB and go to the APP tab, then open the Database Explorer.
2. Click on "Configure Database Source" and then "Configure ODBC Data Source."
3. In the System DNS tab, click Add.
4. Choose MySQL ODBC ANSI Driver and click OK.
5. Provide the following information:
   - Datasource Name: matpdcdb (Your database name)
   - TCP/IP Server: localhost
   - Username: root
   - Password: Your database password (e.g., root)
   - Database: matpdc (selected schema from MySQL Workbench)
6. Click OK and close the Database Explorer window.

## MATLAB Code

Use the following MATLAB code to test the connection and write to the database:

```matlab
% Establish a connection to the database
conn = database('matpdcdb', 'root', 'root');

% Display the connection properties
disp(conn);

timeVector = repmat(datetime('2023-11-13 09:53:51', 'Format', 'yyyy-MM-dd HH:mm:ss'), 3, 1);
var1Vector = repmat([1.6999e9], 3, 1);
var2Vector = repmat([0.767; 0.775; 0.783], 1, 1);

% Create the table
Data = table(timeVector, var1Vector, var2Vector, 'VariableNames', {'PMU_time', 'Var1', 'Var2'});

sqlwrite(conn, tablename, Data);

% Close the database connection
close(conn);
