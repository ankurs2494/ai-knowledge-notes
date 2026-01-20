1️⃣ ip a | grep eth1
Use case: Interface & IP validation (Layer 1–3)
When to use
    • A service is unreachable and you suspect network/interface issues
    • After VM/server boot
    • After changing network config (Netplan, NetworkManager, ifcfg)
    • Verifying the correct interface has an IP
Questions it answers
    • Does eth1 exist?
    • Is it UP?
    • Does it have an IP address?
    • IPv4 / IPv6 assigned?
Typical scenarios
    • Server can’t reach or be reached by other systems
    • Application binding fails due to missing IP
    • Wrong NIC being used
Example flow

ip a | grep eth1
If eth1 has no IP or DOWN, stop here → fix networking.

2️⃣ ss -tulnp | grep 1025
Use case: Service & port validation on local host (Layer 4–7)
When to use
    • Application failed to start
    • Port conflict suspected
    • Verifying a service is actually listening
    • Checking which process owns a port
Questions it answers
    • Is port 1025 listening?
    • TCP or UDP?
    • Which process & PID is bound?
    • Is it bound to 127.0.0.1 or 0.0.0.0?
Typical scenarios
    • nc from another host fails
    • Service shows “started” but not reachable
    • Firewall seems open but connection still refused
Example flow

ss -tulnp | grep 1025
Common findings:
    • Listening on 127.0.0.1 → remote access won’t work
    • No output → service not running
    • Wrong process → port conflict

3️⃣ nc -zv <ip-address> <port>
Use case: Connectivity test between hosts (Layer 4)
When to use
    • Testing remote access to a service
    • Verifying firewall / security group rules
    • Network path troubleshooting
    • After deploying a new service
Questions it answers
    • Can I reach the port remotely?
    • Is it open, closed, or filtered?
    • Is routing/firewall blocking traffic?
Typical scenarios
    • Application works locally but not remotely
    • Firewall change validation
    • Load balancer / VIP testing
Example flow

nc -zv 10.0.0.5 1025
Results interpretation:
    • Succeeded → network path OK
    • Refused → service not listening
    • Timed out → firewall / routing issue





🔄 Real-World Troubleshooting Flow (Best Practice)

Scenario: Application on port 1025 not reachable

Step 1️⃣ Check network interface

ip a | grep eth1
✔ Interface UP and IP assigned?
❌ Fix NIC/IP if not.

Step 2️⃣ Check service locally

ss -tulnp | grep 1025
✔ Port listening?
✔ Correct IP (0.0.0.0)?
❌ Restart/fix app if not.

Step 3️⃣ Test remote connectivity

nc -zv <server-ip> 1025
✔ Connection succeeds → app OK
❌ Timeout → firewall
❌ Refused → service issue

🧠 Quick Decision Table
Problem Question	Command to Use
Is my NIC up and has IP?	`ip a
Is my service listening?	`ss -tulnp
Can another host reach my port?	nc -zv <ip> <port>
Which process uses this port?	ss -tulnp
Is firewall blocking traffic?	nc -zv
App works locally but not remotely	ss ➜ nc

🧩 Summary Logic
    • ip a → Can this host talk on the network?
    • ss → Is the service ready to accept connections?
    • nc → Can another host actually connect?
