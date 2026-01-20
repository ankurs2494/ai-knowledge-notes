
📘 Runbook 1: Public Service Not Reachable (Cloud VM)

Symptoms
    • Service unreachable from internet
    • Timeout from browser / nc
    • Monitoring alert triggered

Step 1️⃣ Instance Health
AWS
    • EC2 → Instance state = running
    • System & instance checks = passed
Azure
    • VM → Status = Running
GCP
    • VM → Status = Running

Step 2️⃣ OS-Level Validation (Inside VM)

ip a
ss -tulnp | grep <port>
✔ Interface UP
✔ IP assigned
✔ Service listening on 0.0.0.0

Step 3️⃣ Cloud Firewall Rules
Cloud	Check
AWS	Security Group inbound rule
Azure	NSG inbound rule
GCP	VPC Firewall rule
✔ Port allowed
✔ Correct source CIDR
✔ Correct protocol (TCP/UDP)

Step 4️⃣ Network Path Validation

nc -zv <public-ip> <port>
Result	Meaning
Success	App OK
Timeout	Firewall / routing
Refused	Service down

Step 5️⃣ Routing
    • Public subnet?
    • Internet Gateway attached?
    • Route 0.0.0.0/0 present?

Root Causes
    • Missing firewall rule
    • Service bound to localhost
    • Instance in private subnet


📘 Runbook 2: Private Service Not Reachable (Internal Only)

Symptoms
    • Service reachable locally
    • Not reachable from another VM

Step 1️⃣ IP & Subnet
    • Same VPC/VNet?
    • Correct subnet CIDR?

ip route

Step 2️⃣ Cloud Internal Firewall
    • AWS SG allows source SG
    • Azure NSG allows VNet
    • GCP firewall allows internal CIDR

Step 3️⃣ OS Firewall

iptables -L
firewall-cmd --list-all

Step 4️⃣ Connectivity Test

nc -zv <private-ip> <port>

Root Causes
    • Wrong CIDR in rule
    • SG-to-SG rule missing
    • OS firewall blocking


📘 Runbook 3: Load Balancer → Backend Not Working

Symptoms
    • Load balancer reachable
    • 502 / 504 errors
    • Health checks failing

Step 1️⃣ Backend Health
Cloud	Check
AWS	Target Group health
Azure	Backend pool health
GCP	Backend service health

Step 2️⃣ Health Check Port
    • Same port as app?
    • App responding to health path?

curl localhost:<port>/health

Step 3️⃣ Security Rules
    • LB SG → Instance SG allowed?
    • NSG / Firewall allows LB subnet?

Step 4️⃣ App Binding

ss -tulnp | grep <port>
✔ Bound to 0.0.0.0

Root Causes
    • Health check path wrong
    • Backend port mismatch
    • SG rule missing


📘 Runbook 4: No Internet Access from VM

Symptoms
    • Outbound traffic fails
    • curl google.com times out

Step 1️⃣ Interface & Route

ip a
ip route
✔ Default route exists

Step 2️⃣ NAT / IGW
Cloud	Requirement
AWS	NAT GW (private subnet)
Azure	NAT Gateway
GCP	Cloud NAT

Step 3️⃣ Firewall Egress
    • Outbound allowed?

Root Causes

    • Missing NAT
    • Route table misconfig
    • Egress blocked


📘 Runbook 5: Cross-VPC / VNet Connectivity Broken

Symptoms
    • VMs cannot reach each other
    • Timeouts on private IP

Step 1️⃣ Peering Status
    • Active?
    • No overlapping CIDRs?

Step 2️⃣ Routing Tables
    • Route to peer CIDR exists?

Step 3️⃣ Firewall Rules
    • Allow peer CIDR traffic?

Step 4️⃣ Test

nc -zv <peer-ip> <port>

Root Causes
    • Missing route
    • Firewall blocking
    • Overlapping IP ranges

🎯 Interview-Ready Cloud Answer
    “In cloud networking issues, I validate the stack from OS networking to cloud firewall rules, routing tables, and finally load balancer health checks. I use ss and nc inside the VM and security group or NSG validation at the cloud layer.”

🧠 Cloud Networking Mental Model


