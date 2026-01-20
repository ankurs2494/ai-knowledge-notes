🧠 Zero-Trust Core Principle (Interview Gold)

    Never trust the network. Always verify identity, device, and policy.
    
This means:
    • No open CIDRs (0.0.0.0/0)
    • No implicit trust inside VPC/VNet
    • Access = Identity + Policy + Context



📘 Runbook 1: Zero-Trust Service Access Failure (Internal App)

    Symptoms
        ○ App reachable from some services but not others
        ○ No public IP involved
        ○ Timeouts despite same VPC
    
    Step 1️⃣ Identity Verification (MOST IMPORTANT)
    
        Platform	Check
        AWS	IAM role attached to caller
        Azure	Managed Identity
        GCP	Service Account
            
        ✔ Correct identity
        ✔ No permission drift
        ❌ If identity is wrong → network checks are irrelevant
    
    Step 2️⃣ Policy Engine Check
    
        Platform	Policy
        AWS	IAM policy / Resource policy
        Azure	Azure RBAC
        GCP	IAM bindings
            
        ✔ Explicit Allow
        ✔ No explicit Deny
    
    Step 3️⃣ Network Micro-Segmentation
    
        ○ Security Groups / NSGs allow identity-based source
        ○ No CIDR-based trust
    
        ALLOW: source = SG-App → SG-DB
DENY: everything else

    
    Step 4️⃣ Service Listening
    
        ss -tulnp | grep <port>
        ✔ Bound to 0.0.0.0
        ✔ Correct port
    
    Root Causes
        ○ Wrong IAM role
        ○ Missing resource policy
        ○ Overly restrictive SG rule


📘 Runbook 2: AWS PrivateLink Service Not Reachable

    Symptoms
        ○ Endpoint created
        ○ DNS resolves
        ○ Connection timeout
    
    Step 1️⃣ DNS Resolution
        
        dig <service-name>
        ✔ Resolves to private IP
        ❌ Public IP → PrivateLink misconfigured
    
    Step 2️⃣ Endpoint State
        ○ Endpoint = Available
        ○ Correct subnet selection
        ○ Private DNS enabled (if needed)
    
    Step 3️⃣ Service Provider Side (Critical)
        ✔ Network Load Balancer healthy
        ✔ Target group healthy
        ✔ Listener port correct
    
    Step 4️⃣ Endpoint Security Group
        ✔ Inbound allows service port
        ✔ Source = consumer VPC CIDR / SG
    
    Step 5️⃣ OS-Level Test
    
        nc -zv <privatelink-dns> <port>
    
    Root Causes
        ○ NLB not healthy
        ○ Missing SG on endpoint
        ○ Private DNS disabled


📘 Runbook 3: Azure Private Endpoint Access Issue

    Symptoms
        ○ Name resolves
        ○ Connection fails
    
    Step 1️⃣ Private DNS Zone
        ✔ Linked to VNet
        ✔ Correct record present
    
    Step 2️⃣ Endpoint Approval
        ✔ Connection approved by service owner
    
    Step 3️⃣ NSG Rules
        ✔ Allow traffic from VNet
        ✔ Correct port
    
    Root Causes
        ○ DNS zone not linked
        ○ Endpoint not approved
        ○ NSG blocking


📘 Runbook 4: GCP Private Service Connect Failure

    Symptoms
        ○ PSC endpoint created
        ○ Timeout from consumer
    
    Step 1️⃣ Forwarding Rule
        ✔ Region matches service
        ✔ IP allocated
    
    Step 2️⃣ Firewall Rules
        ✔ Allow from consumer project
        ✔ Correct tag/service account
    
    Root Causes
        ○ Region mismatch
        ○ Firewall rule missing


🔥 Zero-Trust Incident Example (Interview Story)

    Incident
        Internal service outage despite same VPC.
    Root Cause
        IAM role rotated → service lost permission to access PrivateLink endpoint.
    Fix
        ○ Updated IAM policy
        ○ No network changes required
    Lesson
        Zero-Trust failures look like network issues but are identity issues.

🧠 Zero-Trust Troubleshooting Order (VERY IMPORTANT)

    1️⃣ Identity
    2️⃣ Policy
    3️⃣ DNS
    4️⃣ Network path
    5️⃣ OS / Service
    🚫 Never start with firewall rules.

🎯 Interview-Ready One-Liners

    • “In Zero-Trust, reachability failures are often IAM or policy related, not networking.”
    • “PrivateLink removes routing but not authorization.”
    • “DNS success doesn’t mean access success.”

🧩 Zero-Trust Mental Model

    
