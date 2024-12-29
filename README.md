# self_signed_certificate
This method allows you to generate a self-signed certificate using PowerShell and sign your files like exe file 

1 Generate Thumbprint
```PowerShell
 New-SelfSignedCertificate -Type Custom -Subject "CN=Caphyon, o=Caphyon, C=US" -keyUsage DigitalSignature -FriendlyName "My Friendly Cert Name" -CertStoreLocation "Cert:\CurrentUser\My" -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.3", "2.5.29.19={text}")
```

Identify the Certificate
```PowerShell
$cert = Get-ChildItem -Path Cert:\CurrentUser\My | Where-Object { $_.FriendlyName -eq "My Friendly Cert Name" }
```

Export the Certificate to a PFX File
```PowerShell
# Define the password for the PFX file
$pfxPassword = ConvertTo-SecureString -String "yourpassword" -Force -AsPlainText

# Export the certificate to a PFX file
Export-PfxCertificate -Cert $cert -FilePath "C:\savepath\YourCertificate.pfx" -Password $pfxPassword
```


 after all, Download `Windows SDK` from [Microsoft web Windows SDK](https://developer.microsoft.com/en-us/windows/downloads/windows-sdk/).

install it and uncheck all of them except the `windows SDK siging Tools for Desktop`
![Screenshot 2024-12-29 180758](https://github.com/user-attachments/assets/e6102cdf-c6a5-4188-9a35-a4ecbe0133eb)

Open PowerShell and navigate into this dirctory:
```Powershell
cd C:\Program Files (x86)\Windows Kits\10\bin\10.0.26100.0\x64
```


```Powershell
signtool sign /f "C:\path\to\YourCertificate.pfx" /p "12345" /fd SHA256 /t http://timestamp.digicert.com "E:\path\To\yourexefile"
```


