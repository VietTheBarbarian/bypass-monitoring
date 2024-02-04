Configure proxy server to get over monitoring on network
![image](https://github.com/VietTheBarbarian/bypass-monitoring/assets/56415307/c666f17e-a89f-4ae6-8bb0-7cbcecd8a3da)

Than test with download script
with proxy and without proxy
![image](https://github.com/VietTheBarbarian/bypass-monitoring/assets/56415307/f2682c33-52a6-4c56-b803-7581c00c27c2)

Use $wc.proxy = $null to remove proxy

To add custom Header agent to play around with analyst
$wc.Headers.Add('User-Agent', "This chrome or firefox or????") 
![image](https://github.com/VietTheBarbarian/bypass-monitoring/assets/56415307/4152f49b-174d-4d4e-98e2-a6561ba325ad)
