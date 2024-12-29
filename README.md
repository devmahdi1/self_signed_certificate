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


1. Download `Windows SDK` from [Microsoft web Windows SDK](https://developer.microsoft.com/en-us/windows/downloads/windows-sdk/).
2. 
