1️⃣ Why DNS Exists

    The problem
        ○ Humans like names: google.com
        ○ Computers need numbers: 142.250.72.14
    
    DNS solves this:
        DNS translates names → IP addresses
        
    Without DNS:
        ○ You’d need to memorize IPs
        ○ The internet would be unusable


2️⃣ What Is DNS?

    DNS (Domain Name System) is a distributed phone book for the internet.
    
        ○ Name in → IP out
        ○ Request → Response (like everything else)


3️⃣ DNS Is NOT One Server

    DNS is a hierarchy.
    
    Levels:
        a. Root servers (.)
        b. TLD servers (.com, .org)
        c. Authoritative servers (owner of domain)
    
    No single point of failure.

4️⃣ DNS Resolution Flow (Very Important)

    When you type: www.example.com
    
    Step-by-step:
    
        1️⃣ Browser checks local cache
        2️⃣ OS checks DNS cache
        3️⃣ Ask recursive resolver (ISP / cloud DNS)
        4️⃣ Resolver asks:
            § Root server → “Who handles .com?”
            § TLD server → “Who handles example.com?”
            § Authoritative server → “What is the IP?”
5️⃣ IP returned to browser
6️⃣ Browser connects using IP
    
    💡 This all happens in milliseconds.

5️⃣ DNS Records (You MUST Know These)
    
    A Record
        example.com → 93.184.216.34
        Maps name → IPv4
    
    AAAA Record
        example.com → IPv6 address

    
    CNAME
        www.example.com → example.com
        Alias to another name
    
    MX
        Mail servers for a domain
    
    TXT
        Text data (verification, SPF, DKIM)

6️⃣ DNS Uses UDP (Mostly)

        ○ Default: UDP port 53
        ○ Fast and lightweight
        
    Uses TCP when:
        ○ Response is large
        ○ Zone transfers
        ○ DNSSEC

7️⃣ TTL (Time To Live)

    TTL tells how long a DNS answer can be cached.
        
    Example:
    TTL = 300 seconds
    
    Means:
        ○ Changes won’t be seen immediately
        ○ DNS issues can “persist”

8️⃣ Internal vs Public DNS

    Public DNS
        ○ google.com
        ○ Resolved via internet DNS
    
    Internal DNS
        ○ Used inside companies / clouds
        ○ service.internal
        ○ Not publicly accessible

9️⃣ Common DNS Problems (Real World)

    

🔟 DNS Is Layer 7 (But Affects Everything)

    DNS itself is:
        ○ Application layer
    
    But failure looks like:
        ○ Network issue
        ○ App issue
        ○ Timeout
    
    This is why DNS is tricky.

🧠 Mental Model (Lock This In)

    Name → DNS → IP → TCP → Application

    No DNS = no internet.

✅ Check Your Understanding

    You should confidently answer:

        ○ Why DNS exists
        ○ Difference between A and CNAME
        ○ What TTL means
        ○ Why DNS uses UDP
        ○ Why DNS issues are hard to debug