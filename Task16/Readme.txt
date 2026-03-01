Task 16: RDS Database + SQL Workbench Connection & Queries

Objective
Deploy an Amazon RDS MySQL database and connect it using SQL Workbench to execute SQL queries.

Steps
1. Launch RDS Instance

Opened AWS RDS → Create Database.
Engine: MySQL (Free Tier).
DB Identifier: Database-1
Master Username: pragya
Storage: 20 GB
Public Access: Enabled
Used default VPC.
Launched instance and waited until status Available.
Copied the RDS endpoint.

2. Connect via SQL Workbench

Created new connection:
Hostname: <RDS Endpoint>
Port: 3306
Username: pragya
Password: <YourPassword>
Tested and saved successful connection.

3. Execute SQL Queries

Verified table creation and data insertion.

Outcome

RDS instance launched and accessible.
SQL Workbench connected successfully.
Database, table, and records created correctly.