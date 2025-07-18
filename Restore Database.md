* Create new database
	* `ARCOSDB`
		* Add path of folder `ARCOSDB` in `C:/`
	* `ARCOSRDPDB`
		* Add path of folder in `ARCOSRDPDB` `C:/`
* Restore Blank DB
	* `ARCOSDB`
	* `ARCOSRDPDB`
* Execute `ARCOSDBUpdates from 4.8.1.0 to 4.8.5.4` `12,694 KB`
* Check version of database 
	* `select * from sso_arcos_activex_setting`
* Execute `4850_U4 to SP4.0_HF3_Consolidated Script`
* Execute `4850_U4_SP4.0_HF4`
* Execute HF queries
* Execute users query to create a local domain `ARCOSAUTH` and local user `Arcosadmin`.