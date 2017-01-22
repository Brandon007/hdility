# HDility

Nothing special.

I usually wrote scripts to fasten my geek life.

Now I'm putting them here one by one to share.

## installMOTD
- A script to install MOTD on Debian.
- Preview:

    ![](https://haodong.me/images/contents/2017-01-21-debian-motd.png)

- Usage: `wget https://raw.githubusercontent.com/haodong/hdility/master/installMOTD.sh - | sh`
- [Readmore](https://haodong.me/post/2017-01-21-debian-motd.html)

## NATctl
- A controller to add/list/reset Traffic Transfer through iptables.
- Usage:
```
> NATctl -h
This script can help you handle Traffic Transfer through iptables.
Usage: iptNAT [-c $cmd] [-i #ID] [-f @IP] [-p #Port] [-t @IP] [-b #Port] [-u]
    -c: Give a command to implement. Available commands are:
        add: Add new rules.
        list: List your NAT iptables(PREROUTING and POSTROUTING).
        reset: Reset the two iptables, cleaning all added Traffic Transfer rules.
    -i: Insert on the #IDth line of chain.
    -f: From the IP. By default use 'dig' function to detect its public IP. Must be specified if the host has multiple public IPs.
    -p: From the Port.
    -t: To the IP, namely the target IP address.
    -b: To the Port, namely the target port.
    -u: With UDP mode. By default use TCP only.

The code was written by Hao Dong under GPL-3.0 License.
```
- Example:
    1. If a user from host A want to access host C (1.1.1.1), but the traffic between A and C is two slow to work.
    2. Fortunately there is another host B (0.0.0.0), whose traffic torward host C is faster than A.
    3. Also the route between A and B is very good.
    4. Then the user should use the following code at host B.
```
> NATctl -c add -f 0.0.0.0 -p 60001 -t 1.1.1.1 -b 22
Adding TCP rules ...
Done.

## To revert
> NATctl -c reset
This will clean up all rules on chains of PREROUTING and POSTROUTING.
Are you sure?(y/n)? y
Cleaning ...
Done.
```
