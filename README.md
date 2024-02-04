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
