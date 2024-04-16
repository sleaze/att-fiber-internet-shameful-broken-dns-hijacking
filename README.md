# [att-fiber-internet-shameful-broken-dns-hijacking](https://github.com/sleaze/att-fiber-internet-shameful-broken-dns-hijacking)

A collection of notes about AT&amp;T hijacking DNS and breaking local hostname resolution.

> TheBeeZee commented on Dec 13, 2023
> 
> For me, the DNS Error Assist option works exactly the opposite of what it indicates: if it is on, the AT&T DNS server doesn't hijack unknown domains. If it is off, it does.

ZOMG!!!!! THIS IS INSANE, I just tried the same thing - *turning _ON_ DNS Error Assist* on my AT&T web profile settings, and immediately now instead of:

> $ ping teledildonix
> PING teledildonix (143.244.220.150) 56(84) bytes of data.
> 64 bytes from 143.244.220.150: icmp_seq=1 ttl=47 time=80.1 ms
> 64 bytes from 143.244.220.150: icmp_seq=2 ttl=47 time=131 ms
> 64 bytes from 143.244.220.150: icmp_seq=3 ttl=47 time=88.4 ms
> ^C
> --- teledildonix ping statistics ---
> 3 packets transmitted, 3 received, 0% packet loss, time 2007ms
> rtt min/avg/max/mdev = 80.156/100.183/131.956/22.719 ms

(Note: The above is with error assist OFF, and this result is really bad because ATT is still hijacking the LAN local hostname DNS resolution and replacing it with some Digital Ocean IP address instead of returning the appropriate 192.168.1.x result, basically the same thing poor [bshosey](https://forums.att.com/conversations/att-internet-account/can-not-connect-to-internal-local-machines-by-hostname-i-can-by-ip-address/65b44ee7abeda37c5afd8565) and countless others have been running into _for years_.

After turning it _ON_, I'm getting:

> $ ping teledildonix
> ping: teledildonix: Name or service not known

> $ ping teledildonix.attlocal.net
> ping: teledildonix.attlocal.net: Name or service not known

So, it's still super broken, but as noted by [TheBeeZee](
https://gist.github.com/CollinChaffin/24f6c9652efb3d6d5ef2f5502720ef00?permalink_comment_id=4792579#gistcomment-4792579), the setting behavior appears to be the opposite of what the AT&T portal and Internet at large claim.

Btw, this is with a BWG-500 router and AT&T fiber 1000 service.  Yesterday the local DNS resolution was working fine, then there was a long power outage for most of the day.  After everything came back online, local hostname DNS queries are 100% failing.

The only reliable solution appears to be running your own router behind AT&T's BWG router-modem-all-in-one.  What a pain.

---

A few useful reference links\*:

- https://gist.github.com/CollinChaffin/24f6c9652efb3d6d5ef2f5502720ef00
- https://kagi.com/search?q=bwg-500+local+hostname+not+resolving+143.244.220.150
- https://kagi.com/search?q=att+fiber+local+hostname+not+resolving+143.244.220.150

\*Google is apparently now useless for finding info on the Internet beyond very basic queries for stackoverflow or reddit, I had to use Kagi to discover anything useful on this topic.</rant>

