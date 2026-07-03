# Assignment 2: Soft Deletes vs Hard Deletes

**Real-world system where Soft Deletes are required**

**Example: Social Media App (e.g., Instagram) — deleting a post or account**

When a user deletes a post or deactivates their account, the system doesn't actually erase the data right away. Instead, it just marks it with something like `is_deleted = true` or `deleted_at = timestamp`, and the app hides it from view.

Why soft delete makes sense here:
- Users often want to **recover** something they accidentally deleted (like restoring a deactivated account within a certain window).
- The platform may need the data for **legal/compliance reasons** (e.g., content moderation, investigations).
- It helps with **analytics** — the business might still want to track deleted content for insights, without showing it to users.
- It avoids **breaking references** — if a post is hard deleted but comments/likes still reference it, that could cause errors. Soft delete keeps things intact behind the scenes.

**Real-world system where Hard Deletes are preferred**

**Example: Banking system — removing sensitive/temporary data, or GDPR-related user data removal requests**

If a user requests their personal data be permanently erased (like under GDPR's "right to be forgotten"), the system needs to actually remove it from the database, not just hide it.

Why hard delete makes sense here:
- **Legal requirement** — laws like GDPR require that certain data be completely and irreversibly deleted upon request, not just hidden.
- **Security** — sensitive data (like old authentication tokens, temporary OTPs, or expired session data) shouldn't stick around in the database even in a hidden state, since it could be a security risk if ever exposed.
- **Storage/performance** — keeping large volumes of unnecessary soft-deleted data forever can bloat the database and slow things down over time, so some systems periodically hard delete old soft-deleted records.

**In short:** Soft deletes are great when you might need to recover data or keep a history, like user-generated content. Hard deletes are necessary when data absolutely must be gone — for legal compliance, security, or to keep the database clean.
