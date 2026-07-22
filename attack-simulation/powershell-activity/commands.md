$command = 'Get-Process'
$bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
$encoded = [Convert]::ToBase64String($bytes)

Run : powershell.exe -EncodedCommand <Base64String>
