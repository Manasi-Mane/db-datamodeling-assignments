# Assignment 1: Indexing on the Orders Table

**Table: orders**
Columns: id, user_id, status, created_at

**Suggested Indexes**

1. **Primary Key Index on `id`**
   This is usually automatic since `id` is the primary key, but it's worth mentioning — it uniquely identifies each order and speeds up lookups by order ID.

2. **Index on `user_id`**
   Since we'll often need to fetch all orders placed by a specific user (like showing order history on a profile page), indexing this column speeds up that lookup significantly instead of scanning the whole table.

3. **Index on `status`**
   Orders are often filtered by status — like showing all "pending" or "delivered" orders. An index here makes those filtered queries much faster, especially as the table grows.

4. **Index on `created_at`**
   This is useful for queries that sort or filter by date, like showing recent orders or generating reports for a specific time range.

5. **Composite Index on `(user_id, status)`** (optional, but useful)
   If we frequently query "get all pending orders for a specific user," a composite index on both columns together is more efficient than two separate indexes, since the database can use both conditions in a single lookup.

**Why these indexes?**

Indexes help the database find rows faster without scanning the entire table row by row. Without them, every query — even a simple filter — would have to check every single row, which gets really slow as the table grows to thousands or millions of orders.

I chose `user_id`, `status`, and `created_at` because these are the columns most likely to be used in `WHERE` clauses, `JOIN`s, or `ORDER BY` — the fields that make queries "search-heavy." The primary key index is automatic and just makes sure lookups by `id` stay fast.

That said, indexes aren't free — they take up extra storage and slow down `INSERT`/`UPDATE` operations slightly since the index also needs updating. So the idea is to index only the columns that are actually queried often, not everything.
