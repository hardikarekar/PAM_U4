* Install Win Vaulting Service.
* Enter into Password Change Defaults under tools menu.
	* Enter CPCS details 
		* Enter IP address of Windows domain
		* Enable CPCS
		* Enter port `45045`
* In Global Configuration
	* Change configuration value of `Change password - No of User's authentication` to `1`
* Check if Win Vaulting Service is running.
* If yes then
	* Go into password manager
		* Select Service Group
			* Enter user, domain and password
				* User: `arcosadmin` domain: `ARCOSAUTH` password: `********`
			* Click `Authorize User`
		* Click on Search and your service which you had created for Windows RDP will pop up.
			* Enter ARCON PAM Windows Password Change Service Port: `45045`
			* Start Password Change Process.
		* Your password will rotate internally using port `45045`. 
* If you want to rotate password through gateway port `45045` has to be open and be added in inbound rules in firewall.