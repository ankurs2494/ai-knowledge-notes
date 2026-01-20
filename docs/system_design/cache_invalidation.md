📌 What is Cache Invalidation?

    Cache invalidation is the process of removing or updating cached data before it naturally expires, when the original data changes — so users don’t see outdated (“stale”) information.
    🎯 Goal: Always serve fresh and correct data, not stale cached copies.

🤯 Why Is It Hard?

    In distributed systems, the same data can be cached in many places (servers, CDNs, browsers).
    Making sure every copy is updated at the right time is complex.
    Famous quote:
        “There are only two hard things in Computer Science: cache invalidation and naming things.”

🔁 Common Cache Invalidation Strategies

    Strategy	How It Works	Example Use Case
    TTL (Time-To-Live) ⏱️	Cache expires after a fixed time	Weather data updates every 10 mins
    Write-Through ✍️	Update cache + DB together	Banking balances
    Write-Around 🚫	Write only to DB, cache updated later	Heavy write systems
    Pub/Sub 📡	Events notify all caches to invalidate	Microservices, CDNs

🔹 1. Time-To-Live (TTL)
    Cache auto-expires after a set time.
    
    Example:
    Product price cached for 5 minutes.
    
    User visits page → cache used
After 5 min → cache expires → fetch fresh price

    ✔ Simple
    ❌ Data may be stale briefly

🔹 2. Write-Through
    Update cache and database together.
    
    Example:
    User updates profile name → DB and cache updated immediately.
    ✔ Always fresh
    ❌ Slower writes

🔹 3. Write-Around
    Write to DB only, cache updated when read again.
    
    Example:
    Log data stored in DB but rarely read → no need to cache immediately.
    ✔ Efficient for write-heavy systems
    ❌ First read is slow

🔹 4. Publish / Subscribe
    Services notify others when data changes.
    
    Example:
    Inventory updated → event published → all caches invalidate that item.
    ✔ Best for distributed systems
    ❌ More complex setup

⚠️ Challenges

    Problem	Explanation
    Multiple caches	Same data in many places
    Network delays	Invalidation messages may be delayed
    Partial failures	Some caches miss updates
    CDN complexity	Global caches hard to sync

    Example failure:
    A CDN in Asia misses the invalidation → shows outdated product price.

🧠 Use Cases

    System	Strategy
    News websites	TTL
    Banking apps	Write-Through
    Logging systems	Write-Around
    Microservices	Pub/Sub
    CDNs	TTL + Invalidation API

📝 One-Line Summary

    Cache invalidation ensures cached data is refreshed when the original data changes, using strategies like TTL, write-through, and event-based updates — especially important in distributed systems to avoid stale data.

💡 Memory Tip

    TTL = Time based
    Write-Through = Always fresh
    Write-Around = Fast writes
    Pub/Sub = Distributed sync


