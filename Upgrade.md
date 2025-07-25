## Database Upgrade
* Create two folders in `C:/Database`
	* `ARCOSDB`
	* `ARCOSRDPDB`
* Restore database in SSMS
	* Right Click on database
		* Restore database `Blank Database`
			* Device option
				* Add path: `C:\New folder\Database Blank\ARCOSDB_Blank.bak`
				* Add MDF and LDF path
					* MDF path
						* `C:\Database\ARCOSDB\ARCOSDB.mdf`
					* LDF path
						* `C:\Database\ARCOSDB\ARCOSDB.ldf`
				*  Add path: `C:\New folder\Database Blank\ARCOSRDPDB_blank.bak`
				* Add MDF and LDF path
					* MDF path
						* `C:\Database\ARCOSRDPDBDB\ARCOSRDPDBDB.mdf`
					* LDF path 
						* `C:\Database\ARCOSRDPDBDB\ARCOSDB.ldf`
			* Database restored to 
				* aas_tmppath_client: `ACM4810`
				* aas_tmppath_server: `ASM4810`
		* Upgrade `U0 to U4`
			* Run this script `ARCOS DBUpdates From 4.8.1.0 To 4.8.5.0.sql`
			* Run this script `ARCOS DBUpdates From 4.8.5.0 To 4.8.5.4.sql`
				* aas_tmppath_client: `ACM4850U4`
				* aas_tmppath_server: `ASM4850U4`
		* Upgrade `U4 to U7`
			* Run this script `ARCOS DBUpdates From 4.8.5.4 To 4.8.5.7.sql`
				* aas_tmppath_client: `ACM4850U7`
				* aas_tmppath_server: `ASM4850U7`
				* aas_base_version: `4850U7`
		* We need to drop the indexes before proceeding for faster query execution:
			* Run this script `1.DropAllNonClusterIndex`
		* Upgrade `U7 to U10`
			* Run this script `4850_U8_U9_U10.sql`
				*  aas_tmppath_client: `ACM4850U10`
				* aas_tmppath_server: `ASM4850U10`
				* aas_base_version: `4850U10`
			* Select `ARCOSRDPDB` database and run this script `4850_U10_ARCOSRDPDB`
				* `ARCOSDB` and `ARCOSRDPDB` both are update to `U10`
		* Upgrade from `U11 to U12`
			* Run this script `4850_U12`
				* aas_tmppath_client: `ACM4850U12`
				* aas_tmppath_server: `ASM4850U12`
				* aas_base_version: `4850U12`
			* Take backup of `ARCOSDB` and `ARCOSRDPDB`
				* Select `ARCOSDB` > Tasks > Backup > Path where you want to save the backup
		* Upgrade from `U12 to U16`
			* Navigate to folder `C:\New folder\Database_Upgrade\Database\4850_U16` and execute the queries in sequence below
				* `1.CreateAlterInsertUpdate`
				* `2. Point_In_TimeScript`
					* `InsertIntoAROCOSLOG`
					* `InsertIntoDBALOG`
					* `insertintoSSO_DBA_LOG_Process`
					* `SSO_Service_Log`
					* `sso_user_log`
				* `3.ProcedureScript`
				* `4.Truncate_purge_Api_logsTables` 
				* `5.AfterVerificationPointInTimeTempTableDrop` 
				* `2.CreateIndex`
				* `4850_U16_HF1 to HF9 consolidated db script`
					* aas_tmppath_client: `ACM4850U16`
					* aas_tmppath_server: `ASM4850U16`
					* aas_base_version: `4850U16`
					* aas_hotfix_version: `HF9`
		* Upgrade `U16_SP2_B35`
			* Navigate to `C:\Newfolder\PAM_U16_SP2_B35\PAM_U16_SP2_B35\PAM_U16_SP2_B35\DBScripts`
				* Copy folders 
					* `0.OldConsolidated`
					* `2.SchemaChanges`
					* `3.Views`
					* `4.Functions`
					* `5.Procedures`
					* `6.DataScripts`
				* to a new folder `C:\New folder\Tools\DB_Executor\DBScript\35`
			* Run db executor
				* Authentication: `SQL Server Authentication`
				* Server IP: `192.168.196.135`
				* Server Port: `1450`
				* Server Name: `192.168.196.135,1450`
				* Database: `ARCOSDB`
				* Username: `dba`
				* Password: `********`
			* Navigate to `C:\New folder\PAM_U16_SP2_B35 to B35.5_Consolidated_Migration\PAM_U16_SP2.0_DIFF_B35_TO_B35.1\DBScript ArconDBDeployment`
				* Copy folders
					* `0.OldConsolidated`
					* `2.SchemaChanges`
					* `3.Views`
					* `4.Functions`
					* `5.Procedures`
					* `6.DataScripts`
					* to a new folder `C:\New folder\Tools\DB_Executor\DBScript\35.1`
				* Run db executor
			* Navigate to `C:\New folder\PAM_U16_SP2_B35 to B35.5_Consolidated_Migration\PAM_U16_SP2.0_DIFF_B35.1_TO_B35.2`
				* Copy folders
					* `0.OldConsolidated`
					* `2.SchemaChanges`
					* `3.Views`
					* `4.Functions`
					* `5.Procedures`
					* `6.DataScripts`
					* to a new folder `C:\New folder\Tools\DB_Executor\DBScript\35.2`
				* Run db executor
			* Navigate to `C:\New folder\PAM_U16_SP2_B35 to B35.5_Consolidated_Migration\PAM_U16_SP2.0_DIFF_B35.2_TO_B35.3`
				* Copy folders
					* `0.OldConsolidated`
					* `2.SchemaChanges`
					* `3.Views`
					* `4.Functions`
					* `5.Procedures`
					* `6.DataScripts`
				* to a new folder `C:\New folder\Tools\DB_Executor\DBScript\35.3`
				* Run db executor
			* Navigate to `C:\New folder\PAM_U16_SP2_B35 to B35.5_Consolidated_Migration\PAM_U16_SP2.0_DIFF_B35.3_TO_B35.4`
				* Copy folders
					* `0.OldConsolidated`
					* `2.SchemaChanges`
					* `3.Views`
					* `4.Functions`
					* `5.Procedures`
					* `6.DataScripts`
				* to a new folder `C:\New folder\Tools\DB_Executor\DBScript\35.4`
				* Run db executor
			* Navigate to `C:\New folder\PAM_U16_SP2_B35 to B35.5_Consolidated_Migration\PAM_U16_SP2.0_DIFF_B34.4_TO_B35.5_WM`
				* Copy folders 
					* `0.OldConsolidated`
					* `2.SchemaChanges`
					* `3.Views`
					* `4.Functions`
					* `5.Procedures`
					* `6.DataScripts`
				* to a new folder `C:\New folder\Tools\DB_Executor\DBScript\35.5`
				* Run db executor
					* Select Path `C:\New folder\Tools\DB_Executor\DBScript\35.5`
			* Navigate to `C:\New folder\fwdmigrationscripts`
				* Copy `fwdmigrationscripts` to `C:\Newfolder\Tools\DB_Executor\DBScript`
				* Run db executor
					* Select Path `C:\Newfolder\Tools\DB_Executor\DBScript\fwdmigrationscripts`
			* Navigate to `C:\Newfolder\U16_SP2_B35.8.24_OCI\U16_SP2_B35.8.24_OCI\Database\MSSQL_Package\DBScripts\ARCONDBScripts`
				* Copy folders
					* `0.OldConsolidated`
					* `2.SchemaChanges`
					* `3.Functions`
					* `4.Views`
					* `5.Procedures`
					* `6.DataScripts`
					* `7.Jobs`
					* `8.Index`
					* `9.Migration`
				* to `C:\New folder\Tools\DB_Executor\DBScript\35.8.24`
				* Run db executor
					* Select Path
						* `C:\New folder\Tools\DB_Executor\DBScript\35.8.24`
			* Navigate to `C:\New folder\U16_SP2_B35.8 Patch 25\U16_SP2_B35.8 Patch 25\Database\MSSQL_Package\DBScripts\ARCONDBScripts`
				* Copy folders
					* `2.SchemaChanges`
					* `4.Views`
					* `5.Procedures`
					* `6.DataScripts`
					* `8.Index`
					* `9.Migration`
				* to `C:\New folder\Tools\DB_Executor\DBScript\35.8.25`
				* Run db executor
					* Select path
						* `C:\New folder\Tools\DB_Executor\DBScript\35.8.25`
			* Navigate to `C:\New folder\U16_SP2_B35.8 Patch 26\U16_SP2_B35.8 Patch 26\Database\MSSQL_Package\DBScripts\ARCONDBScripts`
				* Copy folders
					* `2.SchemaChanges`
					* `5.Procedures`
					* `6.DataScripts`
					* `8.Index`
				* to `C:\New folder\Tools\DB_Executor\DBScript\35.8.26`
				* Run db executor
					* Select path 
						* `C:\New folder\Tools\DB_Executor\DBScript\35.8.26`
			* Navigate to `C:\New folder\U16_SP2_B35.8 Patch 27\U16_SP2_B35.8 Patch 27\Database\MSSQL_Package\DBScripts\ARCONDBScripts`
				* Copy folders
					* `2.SchemaChanges`
					* `3.Functions`
					* `5.Procedures`
					* `6.DataScripts`
				* to `C:\New folder\Tools\DB_Executor\DBScript\35.8.27`
				* Run db executor
					* Select path 
						* `C:\New folder\Tools\DB_Executor\DBScript\35.8.27`

* From `C:\Newfolder\U16_SP2_B35.8.24_OCI\U16_SP2_B35.8.24_OCI\Applications\ARCON Web Components` copy 5 folders in `C:\Arcon Solutions`
	* `Admin Settings`
	* `ARCONAPIGateway`
	* `ARCONPAMAPI`
	* `ARCOSClientManagerOnline`
	* `ARCOSUserAccessLogViewerWeb`
* Create a new folder `ArconMicroservicesStack`