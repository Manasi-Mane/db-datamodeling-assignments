# Assignment 3: Composite Index for Bookings Query

**Query:**

```sql
SELECT * FROM bookings
WHERE doctor_id = ?
AND appointment_date >= ?
AND appointment_date <= ?;
```

This query looks up bookings for a specific doctor, within a given date range.

**Proposed Composite Index**

```sql
CREATE INDEX idx_doctor_date ON bookings (doctor_id, appointment_date);
```

**Why this column order?**

I put `doctor_id` first and `appointment_date` second, and that order actually matters a lot.

The general rule for composite indexes is: columns used for **exact/equality matches** should come first, and columns used for **range conditions** (like `>=`, `<=`, `BETWEEN`) should come after.

- `doctor_id = ?` is an equality match, so putting it first lets the database jump straight to that doctor's bookings instead of scanning everything.
- Once it's narrowed down to just that doctor, `appointment_date` is already sorted within that group, so the range check (`>= and <=`) can be done quickly and efficiently.

If I flipped the order — `appointment_date` first, then `doctor_id` — the index would lose most of its benefit. That's because the range condition on `appointment_date` would already break up the "sorted" order before the database even gets a chance to filter by doctor, forcing it to scan a much wider set of rows.

So `(doctor_id, appointment_date)` lets the database use both conditions together efficiently in a single index lookup, rather than needing to fall back on scanning extra rows.
