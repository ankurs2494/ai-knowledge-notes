
Hands-On Linux Networking: Practice Scenarios
You already know the tools:

ip a
ip route
ss -tulnp
ping
nc
Now let’s answer WHY things fail.

Question 1: Why does ping work but nc fails?

Key insight (memorize this):
	Ping tests reachability (ICMP), not service availability (TCP/UDP ports).

What ping actually tests

ping <ip>
	• Uses ICMP (Layer 3)
	• Checks:
		○ Is the host reachable?
		○ Is routing working?
✔ Network path exists
❌ Says nothing about ports or services

What nc tests

nc -zv <ip> <port>
	• Uses TCP or UDP (Layer 4)
	• Checks:
		○ Is a service listening?
		○ Is the port allowed by firewall?

Common Reasons Ping Works but nc Fails

1️⃣ Service is NOT running

	ss -tulnp | grep <port>
	❌ No output → nothing listening

2️⃣ Firewall allows ICMP but blocks ports
		○ ICMP allowed
		○ TCP/UDP blocked
	
	Very common in production.

3️⃣ Wrong port
		○ App listening on 8080
		○ You tested 80

4️⃣ App bound to localhost only
	
	127.0.0.1:<port>
	Remote access will fail.
	
	Mental model
		○ Ping: Can I reach the host?
		○ nc: Can I reach the service?

Question 2: Why does localhost work but remote fails?

Key insight:
	The service is only reachable inside the host, not from the network.
	
Step-by-step explanation

	→ You test locally:
	
		nc -zv localhost <port>
		✔ Works
	
	→ You test remotely:
	
		nc -zv <server-ip> <port>
		❌ Fails

Common Causes

1️⃣ Service bound to loopback only (MOST COMMON)

	ss -tulnp | grep <port>
	
	Output:
	127.0.0.1:<port>
	
	Means:
		○ App listens only on localhost
		○ External traffic is ignored
	
	✅ Fix: bind to 0.0.0.0

2️⃣ Firewall blocks external traffic

		○ Local connections allowed
		○ External connections blocked
	Check:
		○ OS firewall
		○ Cloud security groups

3️⃣ Wrong IP/interface

	ip a
		○ App bound to IP not assigned
		○ Traffic goes to wrong NIC

4️⃣ Routing issue

	ip route
		○ Missing route
		○ Wrong gateway
	
	Less common but possible.

🧠 Command-to-Problem Mapping

	

🔥 Real Interview Answer (Perfect)

	“Ping only tests ICMP reachability, so it can succeed even if the service or port is down. nc tests Layer 4 connectivity, which fails if the service isn’t listening, the port is blocked, or the app is bound to localhost.”

🧪 Mini Lab (Do This Mentally or Practically)

	1️⃣ Stop a service → ping works, nc fails
	2️⃣ Bind service to 127.0.0.1 → localhost works, remote fails
	3️⃣ Block port in firewall → same result

✅ If this makes sense, you now understand:

		○ OSI layers in practice
		○ Why most “network issues” aren’t network issues
		○ How to debug production outages
