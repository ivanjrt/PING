# PING
Resolving dns or ping Methods via PowerShell

# Pinging from Local PC to External and extracting only the IP
Method 1
``` Javascript
$PingHome   = ping "google.com" -n 1 
$regex      = ‘\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b’
$PingTester = $PingHome | select-string -Pattern $regex -AllMatches | % { $_.Matches } | % { $_.Value }
$HomeIp     = $PingTester[0]
$HomeIp 
```

Method 2
``` Java
$pinger = [System.Net.NetworkInformation.Ping]::new()
$pingerRep = $pinger.Send("google.com") 
$pingerRep.Address.IPAddressToString
```

# Finding out the IP for the local PC
Method 1
``` Java
(Invoke-WebRequest myexternalip.com/raw).content 
```
Method 2
``` Javascript
$wc = new-object System.Net.WebClient
$url="http://myexternalip.com/raw"
$wc.DownloadString($url)
```
# Reverse DNS lookup, keep in mind this will also display more properties within $homeIP such, type of IP and AAAA records...
```Javascript
$PingHomeRtr = (Invoke-RestMethod https://api.hackertarget.com/dnslookup/?q=google.com)
$regex       = ‘\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b’
$HomeIp      = $PingHomeRtr | select-string -Pattern $regex -AllMatches | % { $_.Matches } | % { $_.Value }
$HomeIp   
```



