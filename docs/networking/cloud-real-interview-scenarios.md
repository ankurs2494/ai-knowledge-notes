(Networking • Cloud • Zero-Trust)

1️⃣ Scenario:

    “Ping works but application traffic fails.”
    
    What interviewer is testing
        • OSI layers
        • Troubleshooting order
        • Firewall vs service understanding
        
    Whiteboard Answer (Say This)
        “Ping validates Layer 3 reachability using ICMP. Application traffic uses TCP or UDP at Layer 4. If ping works but the app fails, I check whether the service is listening on the expected port and whether firewall rules allow that port.”
        
    Diagram to draw
    Client → ICMP → Host   ✅
Client → TCP:443 → Host ❌

2️⃣ Scenario:

    “Service works on localhost but not from another machine.”
    
    What interviewer wants
        ○ Bind addresses
        ○ Loopback understanding
        
    Whiteboard Answer
        “If localhost works but remote access fails, the service is likely bound to 127.0.0.1 or the inbound firewall blocks external traffic. I’d verify the listening address and firewall rules.”
        
    Diagram
    127.0.0.1:8080  ✅
0.0.0.0:8080    ❌

3️⃣ Scenario:

    “Private subnet has no internet access.”
    
    What’s being tested
        ○ NAT
        ○ Routing
        ○ Cloud networking basics
        
    Whiteboard Answer
        “Private subnets don’t have a route to the internet. Outbound access requires a NAT gateway and a default route to it. Without NAT, private IPs aren’t internet-routable.”
        
    Diagram
    Private Subnet
   ↓
NAT Gateway
   ↓
Internet


4️⃣ Scenario:

    “Application works via IP but not via DNS.”
    
    What interviewer wants
        ○ DNS understanding
        ○ Not blaming the network blindly
    
    Whiteboard Answer
        “If IP works but DNS fails, the network path is fine. The issue is name resolution—likely incorrect DNS records, resolver configuration, or TTL caching.”
        
    Diagram
    Name ❌ → DNS
IP   ✅ → Service


5️⃣ Scenario:

    “Why is PrivateLink more secure than VPC peering?”
    
    What they’re testing
        • Zero-Trust mindset
        • Attack surface reduction
        
    Whiteboard Answer
        “VPC peering creates network-level trust. PrivateLink exposes only a specific service endpoint with no network transitivity. Combined with IAM, access is identity-based, not network-based.”
        
    Diagram
    Peering: VPC ↔ VPC (wide trust)
PrivateLink: Client → Endpoint → Service


6️⃣ Scenario:

    “Explain Zero-Trust networking.”
    
    This is a make-or-break question
    
    Whiteboard Answer (Memorize)
        “Zero-Trust assumes the network is hostile. Access is never granted based on IP or location. Every request is authenticated and authorized using identity, often with IAM or mTLS.”
        
    Diagram
    Network ≠ Trust
Identity → Policy → Access


7️⃣ Scenario:

    “How does mTLS help in microservices?”
    
    What they want
        ○ Service-to-service security
    
    Whiteboard Answer
        “mTLS provides mutual authentication and encryption. Both client and server prove identity using certificates, which removes reliance on IP allowlists and passwords.”
        
    Diagram
    Service A ↔ mTLS ↔ Service B
(cert verified both sides)


8️⃣ Scenario:

    “Traffic reaches the service but returns 403.”
    
    Trick question (network vs identity)
    
    Whiteboard Answer
        “403 means the network path works. The failure is authorization—likely an IAM policy, token scope, or identity mismatch.”
        
    Diagram
    Network ✅
Identity ❌

9️⃣ Scenario:

    “Where do most production networking outages occur?”
    
    Senior-level question
    
    Whiteboard Answer
        “Most outages occur at security boundaries—firewalls, security groups, route tables, or identity policies—not physical networking.”
    
    🔑 The One Diagram You Should Always Draw
    
            Client
 ↓
DNS
 ↓
Routing
 ↓
Firewall
 ↓
Service
 ↓
Identity / Policy

    If you can explain this diagram clearly, you pass.

🧠 Golden Interview Sentences (Use These)

    • “Ping validates reachability, not service availability.”
    • “Private connectivity does not imply authorization.”
    • “Identity-based access scales better than IP-based trust.”
    • “Most issues aren’t network failures but policy failures.”

🎯 Final Advice (Important)

    Interviewers don’t want:
        ❌ Commands
        ❌ Tool names
        ❌ Vendor jargon
    
    They want:
        ✔ Mental models
        ✔ Clear reasoning
        ✔ Calm troubleshooting flow
    
    You now have that.
