# Linux Tips

## traceroute

> Install
```
sudo apt install tcptraceroute
```

> Usage
```
Usage: traceroute [OPTION...] HOST
Print the route packets trace to network host.

  -f, --first-hop=NUM        set initial hop distance, i.e., time-to-live
  -g, --gateways=GATES       list of gateways for loose source routing
  -I, --icmp                 use ICMP ECHO as probe
  -m, --max-hop=NUM          set maximal hop count (default: 64)
  -M, --type=METHOD          use METHOD (`icmp' or `udp') for traceroute
                             operations, defaulting to `udp'
  -p, --port=PORT            use destination PORT port (default: 33434)
  -q, --tries=NUM            send NUM probe packets per hop (default: 3)
      --resolve-hostnames    resolve hostnames
  -t, --tos=NUM              set type of service (TOS) to NUM
  -w, --wait=NUM             wait NUM seconds for response (default: 3)
  -?, --help                 give this help list
      --usage                give a short usage message
  -V, --version              print program version

Mandatory or optional arguments to long options are also mandatory or optional
for any corresponding short options.

Report bugs to <bug-inetutils@gnu.org>.
```

## tcping

> Install
```
sudo wget http://www.vdberg.org/~richard/tcpping -O /usr/local/bin/tcping
sudo chmod 755 /usr/local/bin/tcping
```
> Usage
```
tcpping v1.7 Richard van den Berg <richard@vdberg.org>

Usage: tcping [-d] [-c] [-C] [-w sec] [-q num] [-x count] ipaddress [port]

        -d   print timestamp before every result
        -c   print a columned result line
        -C   print in the same format as fping's -C option
        -w   wait time in seconds (defaults to 3)
        -r   repeat every n seconds (defaults to 1)
        -x   repeat n times (defaults to unlimited)

See also: man tcptraceroute
```

## mtr

> Install
```
sudo apt install mtr
```

> Usage
```
Usage:
 mtr [options] hostname

 -F, --filename FILE        read hostname(s) from a file
 -4                         use IPv4 only
 -6                         use IPv6 only
 -u, --udp                  use UDP instead of ICMP echo
 -T, --tcp                  use TCP instead of ICMP echo
 -I, --interface NAME       use named network interface
 -a, --address ADDRESS      bind the outgoing socket to ADDRESS
 -f, --first-ttl NUMBER     set what TTL to start
 -m, --max-ttl NUMBER       maximum number of hops
 -U, --max-unknown NUMBER   maximum unknown host
 -P, --port PORT            target port number for TCP, SCTP, or UDP
 -L, --localport LOCALPORT  source port number for UDP
 -s, --psize PACKETSIZE     set the packet size used for probing
 -B, --bitpattern NUMBER    set bit pattern to use in payload
 -i, --interval SECONDS     ICMP echo request interval
 -G, --gracetime SECONDS    number of seconds to wait for responses
 -Q, --tos NUMBER           type of service field in IP header
 -e, --mpls                 display information from ICMP extensions
 -Z, --timeout SECONDS      seconds to keep probe sockets open
 -M, --mark MARK            mark each sent packet
 -r, --report               output using report mode
 -w, --report-wide          output wide report
 -c, --report-cycles COUNT  set the number of pings sent
 -j, --json                 output json
 -x, --xml                  output xml
 -C, --csv                  output comma separated values
 -l, --raw                  output raw format
 -p, --split                split output
 -t, --curses               use curses terminal interface
     --displaymode MODE     select initial display mode
 -g, --gtk                  use GTK+ xwindow interface
 -n, --no-dns               do not resolve host names
 -b, --show-ips             show IP numbers and host names
 -o, --order FIELDS         select output fields
 -y, --ipinfo NUMBER        select IP information in output
 -z, --aslookup             display AS number
 -h, --help                 display this help and exit
 -v, --version              output version information and exit

See the 'man 8 mtr' for details.
```

> Example: IPv4, TCP 30000, no-dns, interface ens4, report mode
```
mtr -4Tnr -I ens4 -P 443 google.com
```

>> Output
```
Start: 2023-02-12T13:04:53+0900
HOST: gcpmc                       Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- ???                       100.0    10    0.0   0.0   0.0   0.0   0.0
  2.|-- 192.145.251.68             0.0%    10    8.3   8.2   2.4  41.9  12.3
  3.|-- 141.101.82.7               0.0%    10    2.3   3.8   1.9  16.3   4.4
        172.71.108.3
  4.|-- 104.18.3.161               0.0%    10    1.6   2.0   1.6   2.3   0.3
```

> Example: UDP 53(DNS), report
```
mtr -urP 53 8.8.8.8
```

>> Output
```
Start: 2023-02-12T13:02:02+0900
HOST: gcpmc                       Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- ???                       100.0    10    0.0   0.0   0.0   0.0   0.0
  2.|-- 142.250.213.59             0.0%    10    2.9   2.2   1.1   3.8   0.9
        142.251.226.135
        142.251.225.81
        142.251.226.183
        142.251.225.79
        142.251.226.133
        108.170.236.213
  3.|-- 216.239.46.9               0.0%    10    1.7   2.1   1.5   2.6   0.4
        172.253.67.163
        216.239.46.15
        172.253.67.165
        72.14.237.51
        172.253.67.219
  4.|-- ???                       100.0    10    0.0   0.0   0.0   0.0   0.0
  ```
