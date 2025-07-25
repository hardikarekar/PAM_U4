## Create your own SSL certificate
* Script to create self-signed certificate for `hardik.local`
* Run this script in PowerShell as administrator.
```powershell
# Define the certificate properties
$certSubject = "CN=hardik.local"
$certPath = "Cert:\LocalMachine\My"
$certFriendlyName = "Hardik Local Certificate"

# Create the self-signed certificate
$cert = New-SelfSignedCertificate `
    -Subject $certSubject `
    -DnsName "hardik.local" `
    -CertStoreLocation $certPath `
    -FriendlyName $certFriendlyName `
    -KeyExportPolicy Exportable `
    -KeyLength 2048 `
    -KeyAlgorithm RSA `
    -HashAlgorithm SHA256 `
    -NotAfter (Get-Date).AddYears(5)

# Export to PFX (includes private key)
$pfxPath = "$env:USERPROFILE\Desktop\hardik.local.pfx"
$pfxPassword = ConvertTo-SecureString -String "P@ssw0rd123!" -Force -AsPlainText

Export-PfxCertificate `
    -Cert $cert `
    -FilePath $pfxPath `
    -Password $pfxPassword

# Export to CER (public key only)
$cerPath = "$env:USERPROFILE\Desktop\hardik.local.cer"
Export-Certificate `
    -Cert $cert `
    -FilePath $cerPath

Write-Host "Certificate creation and export complete."
Write-Host "PFX exported to: $pfxPath"
Write-Host "CER exported to: $cerPath"
```
* Output
	* `hardik.local.pfx`: Private + Public Key (used for server applications)
	* `hardik.local.cer`: Public key only (used for clients or import into browsers)
* To use your `hardik.local.cer` in IIS you need to,
	* Import `.pfx` certificate to local machine store 
	* Bind it to your IIS website over HTTPS (usually port 443)
* Run this script in PowerShell
```powershell
# Define the certificate path and password
$pfxPath = "$env:USERPROFILE\Desktop\hardik.local.pfx"
$pfxPassword = ConvertTo-SecureString -String "P@ssw0rd123!" -AsPlainText -Force

# Import the certificate to LocalMachine\My
$cert = Import-PfxCertificate -FilePath $pfxPath -CertStoreLocation "Cert:\LocalMachine\My" -Password $pfxPassword

# Get the thumbprint
$thumbprint = $cert.Thumbprint

# Ensure IIS module is loaded
Import-Module WebAdministration

# Get existing site (change if needed)
$siteName = "Default Web Site"

# Remove existing HTTPS binding if exists (optional safety)
Get-WebBinding -Name $siteName -Protocol "https" | Remove-WebBinding

# Add HTTPS binding using the new certificate
New-WebBinding -Name $siteName -Protocol https -Port 443 -HostHeader "hardik.local"

# Assign the certificate to the binding using netsh
netsh http add sslcert ipport=0.0.0.0:443 certhash=$thumbprint appid='{00112233-4455-6677-8899-AABBCCDDEEFF}'
```
* Ensure the hostname is resolvable - add it to your `hosts` file
```txt
# Add these lines at the last 
192.168.196.135		hardik.local.com
192.168.196.135		api.hardik.local.com
```
* Test
	* Run this to confirm the HTTPS binding
		* `Get-WebBinding -Name "Default Web Site" -Protocol "https"`
* Import `.pfx` certificate 
	* Press `Win + R`
		* Type `mmc`
	* In MMC window, go to File -> Add/Remove snap-in
	* From left pane, select `Certificates`, click `Add`.
	* Choose `Computer Account`, click `Next` then `Finish`.
