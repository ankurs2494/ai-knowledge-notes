🧠 What are Redis and Memcached?
    Both Redis and Memcached are in-memory key-value data stores used to cache data in RAM so applications can avoid hitting slow databases repeatedly.
    Goal:
    👉 Reduce latency
    👉 Reduce database load
    👉 Improve performance
    
⚡ Memcached — Simple & Fast Cache

    Think of Memcached as: A super-fast temporary storage for simple data.
    
    🔹 Characteristics:
            • Stores only simple strings / blobs
            • Multi-threaded → very fast for read-heavy workloads
            • No persistence → data lost on restart
            • Simple eviction → LRU (Least Recently Used)
    
    🔹 Example:
            Website stores user session info:
session_123 → "logged_in=true"

    If the server restarts, sessions are lost (users may log in again).
    
    🔹 Best Use Cases:
            • User sessions
            • Cached HTML pages
            • API responses
            • Read-heavy, simple workloads
    
🧩 Redis — Powerful & Flexible Data Store

    Think of Redis as: An in-memory database with advanced features.
    
    🔹 Characteristics:
            • Supports complex data types:
                ▪ Lists, Sets, Sorted Sets, Hashes
            • Optional persistence to disk
            • Supports:
                ▪ Pub/Sub messaging
                ▪ Transactions
                ▪ Replication & clustering
            • Configurable eviction (LRU, LFU, TTL)
    
    🔹 Example:
        Leaderboard:
ZADD leaderboard 100 "Alice"
ZADD leaderboard 200 "Bob"
        Redis keeps players sorted automatically.
    
    🔹 Best Use Cases:
            • Leaderboards
            • Job queues
            • Real-time analytics
            • Chat systems
            • Rate limiting
    
📊 Redis vs Memcached Comparison

    Feature	Memcached	Redis
    Data Types	Strings only	Strings, Lists, Sets, Hashes, etc.
    Persistence	❌ No	✅ Optional
    Threading	Multi-threaded	Mostly single-threaded
    Use	Simple cache	Cache + Data store
    Pub/Sub	❌ No	✅ Yes
    Eviction	LRU only	LRU, LFU, TTL
    Complex logic	❌ No	✅ Yes
    
🧠 One-Line Summary
        Use Memcached for ultra-fast, simple caching.
        Use Redis when you need persistence, complex data, or messaging.
    
📝 Final takeaway:

    Scenario	Choose
    Simple page caching	Memcached
    Session storage	Memcached
    Leaderboard	Redis
    Chat system	Redis
    Rate limiting	Redis
    Microservices messaging	Redis
    
💡 Interview Memory Tip:
        Memcached = Memory + Cached pages
        Redis = Rich Data + Durable + Distributed
    
🎯 8–10 Important Interview Questions

    1️⃣ What is the difference between Redis and Memcached?
    Answer: Redis supports complex data structures and persistence, Memcached is simple and purely in-memory.
    
    2️⃣ When would you choose Memcached over Redis?
    Answer: When you need extremely fast, simple, temporary caching without persistence.
    
    3️⃣ Can Redis be used as a primary database?
    Answer: Yes, Redis supports persistence and replication, so it can act as a primary NoSQL database.
    
    4️⃣ What eviction strategies does Redis support?
    Answer: LRU, LFU, TTL-based, random, no-eviction.
    
    5️⃣ Why is Redis considered single-threaded yet very fast?
    Answer: It uses an event-loop and in-memory operations which avoid locking overhead.
    
    6️⃣ What happens to data in Memcached when the server restarts?
    Answer: All data is lost.
    
    7️⃣ What is Redis Pub/Sub used for?
    Answer: Messaging between services, cache invalidation, real-time notifications.
    
    8️⃣ How does Redis persistence work?
    Answer: Using RDB snapshots and AOF (append-only file) logs.
    
    9️⃣ Which one is better for leaderboards and why?
    Answer: Redis, because it supports sorted sets.
    
    🔟 How would you use Redis for rate limiting?
    Answer: Using atomic counters with TTL per user/IP.
