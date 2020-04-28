![Logo](https://i.imgur.com/PyKLAe7.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

Wall of shame (2020-04-28)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
62.102.148.68|-|10
185.220.100.253|tor-exit-2.zbau.f3netze.de|9
185.220.100.252|tor-exit-1.zbau.f3netze.de|9
93.186.170.7|-|9
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|9
92.63.194.104|-|9
51.75.144.43|ns3129517.ip-51-75-144.eu|9
195.206.105.217|zrh-exit.privateinternetaccess.com|9
89.234.157.254|marylou.nos-oignons.net|8
178.73.215.171|178-73-215-171-static.glesys.net|8
185.220.103.7|anatkamm.tor-exit.calyxinstitute.org|8
46.165.245.154|-|8
77.247.181.162|chomsky.torservers.net|8
5.182.211.184|-|8
171.25.193.20|tor-exit0-readme.dfri.se|8
171.25.193.25|tor-exit5-readme.dfri.se|8
114.67.74.50|-|8
62.210.105.116|62-210-105-116.rev.poneytelecom.eu|8
202.29.220.182|-|8
185.220.100.243|tor-exit-16.zbau.f3netze.de|8
185.220.100.240|tor-exit-13.zbau.f3netze.de|8
185.220.100.241|tor-exit-14.zbau.f3netze.de|8
77.247.181.165|politkovskaja.torservers.net|8
5.182.211.180|-|8
