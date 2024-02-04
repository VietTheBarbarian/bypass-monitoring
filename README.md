Configure proxy server to get over monitoring on network
![image](https://github.com/VietTheBarbarian/bypass-monitoring/assets/56415307/c666f17e-a89f-4ae6-8bb0-7cbcecd8a3da)

Than test with download script
with proxy and without proxy
![image](https://github.com/VietTheBarbarian/bypass-monitoring/assets/56415307/f2682c33-52a6-4c56-b803-7581c00c27c2)

Use $wc.proxy = $null to remove proxy

To add custom Header agent to play around with analyst
$wc.Headers.Add('User-Agent', "This chrome or firefox or????") 
![image](https://github.com/VietTheBarbarian/bypass-monitoring/assets/56415307/4152f49b-174d-4d4e-98e2-a6561ba325ad)


Issue you might run in:
PowerShell download cradle running in SYSTEM integrity level
context does not have a proxy configuration set 
example shown below
Despite being connected to the proxy you will not get the proxy address


![image](https://github.com/VietTheBarbarian/bypass-monitoring/assets/56415307/d5aef849-ec04-4e62-8dce-f04343762276)

![image](https://github.com/VietTheBarbarian/bypass-monitoring/assets/56415307/2c55f4b7-c52f-4fdf-b07c-15ae28e18102)

Cause:
PowerShell download cradle running in SYSTEM integrity level
context does not have a proxy configuration set 

To run our session through a proxy we have to create a proxy config for the built in system account. 
We can copy the config from a standard user account 
![image](https://github.com/VietTheBarbarian/bypass-monitoring/assets/56415307/bb33a5ae-1b10-4036-89e3-1e8144890a6a)

Another problem is that we won't be able to see this setting unless we are root not system so the above can't be seen if we have intial 
access BUT we can still map it using powershell.

Fix:
Resolve the following registry
New-PSDrive -Name HKU -PSProvider Registry -Root HKEY_USERS | Out-Null
we can now interact with and query the HKEY_USERS hive

We need to loop through the hiv. 
Registry hives are devided and named after sids of user that existed.
S-1-5-21- is a user account 
To find valid hive we loop through top level entries of the HKEY_USERS until we find one with a matching SID
Than we filter out the lower 10 characters leaving only the sids and omitting the hkey_users string

$keys = Get-ChildItem 'HKU:\'
ForEach ($key in $keys) {if ($key.Name -like "*S-1-5-21-*") {$start = $key.Name.substring(10);break}}


To fetch the content of the registry key, 
Get-ItemProperty
This accept the path of the registry path and key we need and elminiating the need to specify "HKEY_USERS"
To gather proxy server IP address and network port from registry ($proxyAddr)
Assign webproxy class and DefaultWebProxy that is built into all Net.WebClient objects to gather the proxy server ip address and network port from the registry
$proxyAddr=(Get-ItemProperty -Path "HKU:$start\Software\Microsoft\Windows\CurrentVersion\Internet Settings\").ProxyServer

Code added into 
download2.ps1
![image](https://github.com/VietTheBarbarian/bypass-monitoring/assets/56415307/a9b5ecd7-e4a8-4a30-97dc-d7261f6e5999)

![image](https://github.com/VietTheBarbarian/bypass-monitoring/assets/56415307/fd64cd17-a446-403f-92d1-2b9123934c82)
