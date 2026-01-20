=================================================================================
Command filters listening network sockets for port 1025
=================================================================================
    ss -tulnp | grep 1025
    
What each part means
    • ss – socket statistics (modern replacement for netstat)
    • -t – TCP sockets
    • -u – UDP sockets
    • -l – listening sockets
    • -n – show numeric ports/IPs (no DNS resolution)
    • -p – show process using the socket (PID/program name)
    • | grep 1025 – only show lines containing port 1025

What it tells you
It shows:
    • Whether port 1025 is open
    • Whether it’s TCP or UDP
    • Which process and PID is bound to it
    • The local address (e.g. 0.0.0.0:1025, 127.0.0.1:1025, [::]:1025)

If you want to avoid false matches (e.g. 11025):
ss -tulnp sport = :1025

=================================================================================
Command filters your network interfaces to show lines related to eth1
=================================================================================
    ip a | grep eth1
    
What it does
    • ip a (or ip addr) shows all network interfaces and their IP addresses
    • grep eth1 filters the output to only lines containing eth1

Typical output

2: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 ...
    inet 192.168.1.10/24 brd 192.168.1.255 scope global eth1
    inet6 fe80::a00:27ff:fe4e:66a1/64 scope link

This tells you:
    • Interface eth1 exists
    • Whether it’s UP
    • Its IPv4 address (inet)
    • Its IPv6 address (inet6)

More useful variants
To get cleaner or more specific info:

ip -br a | grep eth1     # brief, one-line summary
ip a show eth1             # only eth1, no grep needed
ip -4 a show eth1        # IPv4 only
ip -6 a show eth1        # IPv6 only

=================================================================================
Command uses netcat (nc) to test whether a TCP port is reachable on a remote host.
=================================================================================

    nc -zv <ip-address> <port>
    
What each part means

    • nc – netcat (network utility)
    • -z – zero-I/O mode (don’t send data, just scan)
    • -v – verbose output
    • <ip-address> – target host (IP or hostname)
    • <port> – target port (e.g. 22, 80, 1025)

Possible outputs

    Port open / reachable: Connection to 192.168.1.10 1025 port [tcp/*] succeeded!
    Port closed: nc: connect to 192.168.1.10 port 1025 (tcp) failed: Connection refused
    Filtered / blocked (firewall): nc: connect to 192.168.1.10 port 1025 (tcp) failed: Operation timed out
Notes
    • This tests TCP only by default
    • It does not verify the application protocol, only connectivity
    • Requires no service banner or authentication
    
Useful variations

nc -zv <ip> 20-30        # scan a port range
nc -zvu <ip> <port>     # UDP check (less reliable)
nc -w 3 -zv <ip> <port> # 3-second timeout

