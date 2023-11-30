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

  3×3 table

         PMU_time             Var1       Var2 
    ___________________    __________    _____

    2023-11-13 09:53:51    1.6999e+09    0.767
    2023-11-13 09:53:51    1.6999e+09    0.775
    2023-11-13 09:53:51    1.6999e+09    0.783
