* Create two folders in `C:\Database`
	* ARCOSDB
	* ARCOSRDPDB
* Create a new database user
	* General
		* Select SQL Server Authentication
		* Enter login name `pamsqladmin`, password `pass@123`
		* Uncheck Enforce Password Policy
	* Server Roles
		* check db creator
		* check public
	* User Mapping
		* ARCOSDB
			* Select
				* databackupoperator
				* datareader
				* datawriter
				* ddladmin
				* public
		* ARCOSRDPDB
			* Select
				* databackupoperator
				* datareader
				* datawriter
				* ddladmin
				* public
* Restore Database in SSMS
	* Select Device
	* Give Backup Path
		* ARCOSDB_Blank.bak
			* Create two files MDF, LDF 
		* ARCOSRDPDB_Blank.bak
			* Create two files MDF, LDF 
* U1 to U4
	* Run this database script
		* `ARCOS DBUpdates From 4.8.1.0 To 4.8.5.4`
			* Parse the database script
			* Execute the database script
	* Run this database script
		* `ARCOS DBUpdates From 4.8.1.0 To 4.8.5.4`
			* Parse 
			* Execute
	* Run this database script
		* `ARCOS DBUpdates From 4.8.5.4 To 4.8.5.7`