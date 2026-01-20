An SSL (Secure Sockets Layer) certificate is a digital credential installed on a web server to verify a website's identity and enable an encrypted connection. While often still referred to as "SSL," modern websites actually use the more secure successor protocol, TLS (Transport Layer Security). 
Core Functions
    • Encryption: Scrambles data sent between a user's browser and the server (such as passwords or credit card numbers), making it unreadable to anyone who intercepts it.
    • Authentication: Verifies that the website is legitimate and owned by the entity it claims to represent.
    • Data Integrity: Ensures that information is not tampered with during transit. 


Types of SSL Certificates
Certificates are categorized by their validation level and the number of domains they cover: 
    • Validation Levels:
        ○ Domain Validated (DV): The most basic level; only verifies domain ownership. It is often free and issued in minutes.
        ○ Organization Validated (OV): A mid-level option that requires the Certificate Authority (CA) to verify the legal existence of the organization.
        ○ Extended Validation (EV): The highest level of trust, involving a strict background check. It is used by banks and large enterprises to demonstrate maximum legitimacy.
    • Domain Coverage:
        ○ Single Domain: Secures one specific domain or subdomain.
        ○ Wildcard: Secures a primary domain and an unlimited number of its first-level subdomains (e.g., *.example.com).
        ○ Multi-Domain (SAN): Secures multiple distinct domains and subdomains on a single certificate. 
How to Identify a Secure Site
    When a site has a valid certificate, you will see visual cues in the browser: 
    1. HTTPS Prefix: The URL begins with https:// instead of http://.
    2. Padlock Icon: A closed padlock appears next to the URL, which can be clicked to view certificate details.
    3. Warning Messages: Browsers will show a "Not Secure" warning if the certificate is missing, expired, or invalid.
