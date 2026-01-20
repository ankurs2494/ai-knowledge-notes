1️⃣ What Is Routing?

    Definition:
        Routing is the process of deciding where to send a packet next.
        
    Every packet asks:
        “How do I reach this destination IP?”
        
    The answer comes from a routing table.

2️⃣ Routing Table (Concept)

    A routing table is just a list of rules:
    
        
    
    The most important rule:
    0.0.0.0/0 → default gateway

    This means:
        “If I don’t know where to send traffic, send it here.”

3️⃣ What Is a Gateway?

    Definition:
        A gateway is a router that connects one network to another.
        
    Your host says:
        ○ “This IP is not in my subnet”
        ○ “Send it to the gateway”
    
    Without a gateway:
        ❌ You can only talk inside your subnet
        ❌ No internet access

4️⃣ Simple Example

    Host:
    IP: 192.168.1.10/24
Gateway: 192.168.1.1
        ○ To 192.168.1.20 → direct
        ○ To 8.8.8.8 → gateway

5️⃣ Routing Across the Internet

    When sending traffic to the internet:
    
        a. Your host → local gateway
        b. Gateway → ISP router
        c. ISP → backbone routers
        d. Reaches destination network
        e. Response follows route back
    
    Each router only knows:
        “Where to send this packet next”
        
        
    No router knows the whole internet.

6️⃣ What Is NAT?

    Definition:
        NAT (Network Address Translation) changes IP addresses in packets.
        
    Why NAT exists:
        ○ IPv4 address shortage
        ○ Private IPs not internet-routable

7️⃣ Types of NAT (Conceptual)

    → Source NAT (SNAT)
        ○ Used for outbound internet access
        ○ Private IP → Public IP
    
    → Destination NAT (DNAT)
        ○ Used for inbound access
        ○ Public IP → Private IP

8️⃣ NAT in Real Life

    Without NAT (Fails)
    192.168.1.10 → Internet ❌
    
    With NAT (Works)
    192.168.1.10
   ↓
NAT Router (Public IP)
   ↓
Internet

    NAT keeps a mapping table:
        Private IP:Port ↔ Public IP:Port


9️⃣ Cloud Example (Very Important)

    → Private subnet:
        ○ Has private IPs only
        ○ ❌ No internet by default
    
    → Add NAT Gateway:
        ○ Outbound internet works
        ○ Inbound still blocked
    
    → Public subnet:
        ○ Has route to Internet Gateway
        ○ Can receive inbound traffic
    
    Same networking rules, cloud names.

🔟 Routing vs NAT (Key Difference)

    

🧠 Mental Model (Lock This In)

    Host → Routing table → Gateway → NAT → Internet


🔥 Common Beginner Mistakes

    ❌ Thinking NAT = routing
    ❌ Forgetting default gateway
    ❌ Assuming private IPs are internet reachable
    ❌ Debugging firewall before routing

✅ Check Your Understanding
You should confidently answer:
    • What is routing?
    • What is a default gateway?
    • Why NAT is required?
    • Difference between SNAT and DNAT?
    • Why private subnets need NAT gateways?
