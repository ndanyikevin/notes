# 1️⃣ Computed Invoice Totals (❗ VERY IMPORTANT)

## ❓ The problem

Right now you have:

- `invoice_items` (quantity, unit price, tax, discount)
    
- `invoices.total`, `amount_paid`, etc.
    

If totals are **manually entered**, you risk:

- Math inconsistencies
    
- Bugs when items change
    
- Fraud / data corruption
    

👉 **Invoice totals must be derived from items**.

---

## ✅ Correct approach (best practice)

### Rule of thumb

> **Store totals, but never trust manual input.**

We:

- **Compute totals from items**
    
- **Persist the result on the invoice**
    
- Recompute on every mutation
    

---

## 🧠 Where should totals be calculated?

### ❌ Not in the database (usually)

- Triggers are hard to debug
    
- Harder to test
    
- Vendor lock-in
    

### ✅ In the service layer (recommended)

- Predictable
    
- Testable
    
- Framework-agnostic
    

---

## 🧮 Invoice calculation logic (example)

```ts
export function calculateInvoiceTotals(items: {
  quantity: number;
  unitPrice: number;
  taxRate: number;
  discountRate: number;
}[]) {
  let subtotal = 0;
  let taxTotal = 0;
  let discountTotal = 0;

  for (const item of items) {
    const lineBase = item.quantity * item.unitPrice;
    const lineDiscount = lineBase * (item.discountRate / 100);
    const lineTax = (lineBase - lineDiscount) * (item.taxRate / 100);

    subtotal += lineBase;
    discountTotal += lineDiscount;
    taxTotal += lineTax;
  }

  return {
    subtotal,
    discountTotal,
    taxTotal,
    total: subtotal - discountTotal + taxTotal,
  };
}
```

---

## 🧾 When to run this?

- After adding/removing invoice items
    
- Before issuing an invoice
    
- After editing an item
    

---

## ✅ Why store totals at all?

- Faster reads (PDFs, dashboards)
    
- Historical accuracy (prices don’t change)
    
- Accounting compliance
    

---

# 2️⃣ Money Normalization (KES-safe 💰)

## ❓ The problem

Money stored as:

- `numeric`
    
- `decimal`
    
- floating point
    

❌ Risk:

- Rounding errors
    
- Cross-language inconsistencies
    
- Silent bugs
    

---

## ✅ Best practice: **Store money as integers**

### Rule

> **Store smallest unit (cents) as integers**

For Kenya:

- KES → store **cents**
    
- 1,500.75 KES → `150075`
    

---

## 🔧 Schema change example

### ❌ Before

```ts
unitPrice: numeric("unit_price", { precision: 14, scale: 2 })
```

### ✅ After

```ts
unitPriceCents: integer("unit_price_cents").notNull();
```

Same for:

- `subtotal`
    
- `total`
    
- `amountPaid`
    
- `basePay`
    
- `allowance`
    
- `deduction`
    

---

## 🧮 Formatting for UI

```ts
function formatKES(cents: number) {
  return `KES ${(cents / 100).toFixed(2)}`;
}
```

---

## ✅ Why this matters

- No rounding bugs
    
- Easy math
    
- Safe across JS, DB, PDFs, mobile apps
    

Accounting systems **always** do this.

---

# 3️⃣ Soft Deletes (⚠️ Compliance & Safety)

## ❓ The problem

Hard deletes:

```sql
DELETE FROM invoice WHERE id = 5;
```

❌ This is dangerous:

- Audits fail
    
- History lost
    
- Payments orphaned
    

---

## ✅ Solution: Soft deletes

### Add this column

```ts
deletedAt: timestamp("deleted_at");
```

---

## 🗑️ Delete becomes:

```ts
await db
  .update(invoices)
  .set({ deletedAt: new Date() })
  .where(eq(invoices.id, id));
```

---

## 🔍 Query active records only

```ts
.where(isNull(invoices.deletedAt))
```

---

## 🧾 Why this is critical

- Legal compliance
    
- Financial traceability
    
- Undo mistakes
    
- Audit readiness
    

This is **non-negotiable** in finance apps.

---

# 4️⃣ Audit Logs (🧠 Who did what, and when)

## ❓ The problem

Without audit logs:

- You don’t know who edited an invoice
    
- No accountability
    
- Impossible to debug disputes
    

---

## ✅ Audit log model

### `audit_log` table

```ts
import {
  pgTable,
  serial,
  varchar,
  jsonb,
  timestamp,
} from "drizzle-orm/pg-core";

export const auditLogs = pgTable("audit_log", {
  id: serial("id").primaryKey(),
  entity: varchar("entity", { length: 50 }).notNull(),
  entityId: varchar("entity_id", { length: 255 }).notNull(),
  action: varchar("action", { length: 50 }).notNull(),
  performedBy: varchar("performed_by", { length: 255 }),
  before: jsonb("before"),
  after: jsonb("after"),
  createdAt: timestamp("created_at").defaultNow(),
});
```

---

## ✍️ Usage example

```ts
await db.insert(auditLogs).values({
  entity: "invoice",
  entityId: invoiceId.toString(),
  action: "UPDATE",
  performedBy: userId,
  before: oldInvoice,
  after: newInvoice,
});
```

---

## ✅ Why audit logs matter

- Legal disputes
    
- Internal accountability
    
- Debugging
    
- Trust with clients
    

Banks and ERPs **require** this.

---

# 🧠 How this all fits together (big picture)

|Feature|Why it matters|
|---|---|
|Computed totals|Data integrity|
|Integer money|Financial correctness|
|Soft deletes|Compliance & recovery|
|Audit logs|Accountability & trust|

Together, this turns Brandflare into a **real accounting-grade system**, not just a CRUD app.

---

## 🔥 Next steps (recommended)

I can:

1. Refactor **all money columns to cents**
    
2. Add **helper services** (`invoice.service.ts`)
    
3. Add **PDF-safe invoice snapshots**
    
4. Add **permissions per role**
    

Tell me what you want next — you’re building this the _right_ way 💪