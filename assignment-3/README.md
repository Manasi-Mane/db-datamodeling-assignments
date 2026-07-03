# Assignment 3: Normalization

**Why is normalization important? What problems occur if a database is not normalized?**

Normalization is basically about organizing your database properly so you're not storing the same data over and over again. It keeps things clean, consistent, and easier to manage as the database grows.

If you don't normalize your data, you run into a bunch of issues:

- **Redundancy** — the same data (like a customer's name or address) ends up repeated in multiple rows, which wastes space.
- **Update anomalies** — if something changes, like a customer's address, you'd have to update it everywhere it appears. Miss one spot, and now your data is inconsistent.
- **Insertion anomalies** — sometimes you can't add new data without also having unrelated data ready. For example, not being able to add a new product unless it's tied to an order.
- **Deletion anomalies** — deleting one record can accidentally wipe out other useful information. Like if you delete the only order a customer made, you lose all record of that customer too.

Basically, normalization helps avoid these headaches and keeps the database reliable.

---

**Convert the following unnormalized data into 1NF**

Original data:

| Order_ID | Customer_Name | Products |
|----------|---------------|----------|
| 101 | Rahul | Laptop, Mouse |

This isn't in 1NF because the Products column has two values crammed into one cell. To fix it, we split it so each row has just one product:

| Order_ID | Customer_Name | Product |
|----------|---------------|---------|
| 101 | Rahul | Laptop |
| 101 | Rahul | Mouse |

Now each cell holds only a single value, which satisfies the 1NF rule.
