# Assignment 1: Database Types in Real-World Applications

**1. Instagram / Facebook (Social Media Feeds) — NoSQL (Cassandra / DynamoDB)**

These apps deal with tons of data — posts, likes, comments — coming in constantly from millions of users at once. NoSQL databases are a better fit here because they can scale across multiple servers easily and don't force you to stick to a rigid structure, so it's easier to handle this kind of large, fast-moving data.

**2. Banking / Financial Transaction System — SQL (PostgreSQL / MySQL)**

For banking, accuracy matters way more than speed. Every transaction needs to be 100% correct — you can't have money disappearing or duplicating. SQL databases are built for this because they follow ACID properties, which basically guarantee a transaction either happens completely or doesn't happen at all. The structured format also helps maintain proper relationships between accounts and transactions.

**3. Ride-Sharing App Live Location Tracking (e.g., Uber/Ola) — In-Memory Database (Redis)**

Apps like Uber need to track driver locations in real time, and that data keeps changing every few seconds. A regular database would be too slow for this. In-memory databases like Redis store everything in RAM instead of disk, so read/write speeds are super fast — perfect for real-time updates like this.
