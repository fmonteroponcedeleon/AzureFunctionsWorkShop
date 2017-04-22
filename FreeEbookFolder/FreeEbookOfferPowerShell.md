

```powershell
#Datos
$web = Invoke-WebRequest -Uri https://www.packtpub.com/packt/offers/free-learning -UseBasicParsing
$texto = ($web.RawContent -split '<div class="dotd-title">' | select -Last 1)
$title = (($texto -split '</h2>' | select -First 1) -split '<h2>' | select -Last 1).trim()
#Credenciales
$user = 'vmsilvamolina@victorsilva.com.uy'
$pass = (ConvertTo-SecureString 'XXXXXXXXXXXXXX' -AsPlainText -Force)
$cred = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $user, $pass
#Envío de mail 
$date = Get-Date -Format dd/MM
Send-MailMessage -To vmsilvamolina@gmail.com -From vmsilvamolina@victorsilva.com.uy -Subject "Packtpub: Libro gratis - $date" -Body $title -SmtpServer smtp.office365.com -UseSsl -Credential $cred -Port 587
```