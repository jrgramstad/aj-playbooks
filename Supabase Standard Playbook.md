# SUPABASE STANDARD PLAYBOOK
**For Claude Code Sessions**
**Last Updated:** November 26, 2025

---

## CONNECTION DETAILS

### Project Info
| Field | Value |
|-------|-------|
| **Project Name** | AJ Real Estate System |
| **Project ID** | gcuunlxfgtnppnqkikaz |
| **URL** | https://gcuunlxfgtnppnqkikaz.supabase.co |
| **Region** | US East |
| **Dashboard** | https://supabase.com/dashboard/project/gcuunlxfgtnppnqkikaz |

### Credentials
```javascript
// config.js - Use in ALL apps
const config = {
  supabase: {
    url: 'https://gcuunlxfgtnppnqkikaz.supabase.co',
    anonKey: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImdjdXVubHhmZ3RucHBucWtpa2F6Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjE1NzY3MTgsImV4cCI6MjA3NzE1MjcxOH0.8uKySCjd_f8sqOtYAyD2_MyvQIC_2IsYkHE1NoqtQT4'
  }
};
```

---

## CRITICAL RULE: DISABLE RLS

**ALWAYS run this after creating any table:**
```sql
ALTER TABLE table_name DISABLE ROW LEVEL SECURITY;
```

Without this, anonymous users (our apps) can't read/write data.

---

## SHARED TABLES (USE THESE)

These tables already exist. **Reuse them** - don't create duplicates.

### 1. properties (77 records)
**Foundation for everything. All apps reference this.**

```sql
-- Key columns (there are 60+ total)
id SERIAL PRIMARY KEY,
name TEXT UNIQUE NOT NULL,          -- "Oak Creek", "Chatham Forney", etc.
full_address TEXT,
city TEXT,
state TEXT DEFAULT 'TX',
zip TEXT,
county TEXT,

-- Property details
property_type TEXT,                 -- "Single Family", "Townhouse"
bedrooms INTEGER,
bathrooms NUMERIC(3,1),
square_footage INTEGER,
year_built TEXT,
lot_size TEXT,

-- Financial
purchase_price NUMERIC(10,2),
purchase_date DATE,
acquisition_method TEXT,            -- "Auction", "MLS", etc.
mortgage_balance NUMERIC(10,2),
mortgage_payment NUMERIC(10,2),
interest_rate NUMERIC(5,3),
mortgage_lender TEXT,               -- Who originated the loan
loan_servicer TEXT,                 -- Who services it now (often different)

-- Current status
occupancy_status TEXT,              -- "Occupied", "Vacant", "Eviction"
current_tenant TEXT,
lease_end_date DATE,
zillow_value NUMERIC(10,2),
fair_market_rent NUMERIC(10,2),

-- For evictions
jp_court TEXT,                      -- Which JP court handles this property

-- Metadata
active BOOLEAN DEFAULT TRUE,
sort_order INTEGER,
created_at TIMESTAMP DEFAULT NOW(),
updated_at TIMESTAMP DEFAULT NOW()
```

**Usage:**
```javascript
// Get all active properties
const { data } = await supabaseClient
  .from('properties')
  .select('id, name')
  .eq('active', true)
  .order('sort_order');

// Get properties with mortgages
const { data } = await supabaseClient
  .from('properties')
  .select('*')
  .not('mortgage_balance', 'is', null)
  .gt('mortgage_balance', 0);
```

### 2. categories
**Expense/transaction categories**

```sql
id SERIAL PRIMARY KEY,
name TEXT UNIQUE NOT NULL,
active BOOLEAN DEFAULT TRUE,
sort_order INTEGER,
created_at TIMESTAMP DEFAULT NOW()
```

**Current categories include:**
- Gas/Automotive
- Job Supplies
- Storage
- Utilities
- Office Supplies
- Cleaning
- Pest Control
- Mowing
- Maintenance Task
- Other

### 3. cardholders
**Team members (especially those with company cards)**

```sql
id SERIAL PRIMARY KEY,
full_name TEXT NOT NULL,
card_last_4 TEXT,                   -- Last 4 digits of card
role TEXT,                          -- "Owner", "Back Office", "Operations", etc.
active BOOLEAN DEFAULT TRUE,
created_at TIMESTAMP DEFAULT NOW()
```

**Current team:**
- Ashley Gramstad (Owner)
- Jessica (Back Office)
- Thomas Tolbert (Project Manager)
- Christian Rojas (Operations)
- Ryder Holliman (Crew Leader)
- Omar Martinez (Maintenance)
- Jose (Crew Leader)

---

## APP-SPECIFIC TABLES

### Credit Card Transactions App
```sql
CREATE TABLE transactions (
  id SERIAL PRIMARY KEY,
  report_date DATE NOT NULL,
  posted_date DATE NOT NULL,
  transaction_date DATE,
  source TEXT NOT NULL,              -- 'Capital One' or 'Home Depot'
  description TEXT NOT NULL,
  amount NUMERIC(10,2) NOT NULL,
  property TEXT,                     -- References properties.name
  category TEXT,                     -- References categories.name
  cardholder_name TEXT,
  card_last_4 TEXT,
  order_number TEXT,
  store_location TEXT,
  notes TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);
```

### P&L Transactions App
```sql
CREATE TABLE pl_transactions (
  id SERIAL PRIMARY KEY,
  transaction_date DATE NOT NULL,
  description TEXT NOT NULL,
  amount NUMERIC(10,2) NOT NULL,
  type TEXT NOT NULL,                -- 'income', 'expense', 'cash-flow'
  category TEXT,
  property TEXT,
  account TEXT,
  transaction_type TEXT NOT NULL,    -- 'business' or 'personal'
  source TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  modified_at TIMESTAMP DEFAULT NOW()
);
```

### Bill Tracking (TO BE BUILT)
```sql
-- Proposed schema
CREATE TABLE bills (
  id SERIAL PRIMARY KEY,
  property_id INTEGER REFERENCES properties(id),
  bill_type TEXT NOT NULL,           -- 'mortgage', 'utility', 'insurance', 'tax'
  vendor TEXT,                       -- Who we pay
  servicer TEXT,                     -- Who services it (for mortgages)
  amount NUMERIC(10,2),
  due_day INTEGER,                   -- Day of month (1-31)
  payment_method TEXT,               -- 'autopay', 'check', 'online'
  account_number TEXT,
  notes TEXT,
  active BOOLEAN DEFAULT TRUE,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE bill_payments (
  id SERIAL PRIMARY KEY,
  bill_id INTEGER REFERENCES bills(id),
  due_date DATE NOT NULL,
  amount_due NUMERIC(10,2),
  amount_paid NUMERIC(10,2),
  paid_date DATE,
  paid_by TEXT,                      -- Who confirmed payment
  status TEXT DEFAULT 'pending',     -- 'pending', 'paid', 'late', 'overdue'
  confirmation_number TEXT,
  notes TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);
```

### Eviction Tracking (TO BE BUILT)
```sql
-- Proposed schema
CREATE TABLE evictions (
  id SERIAL PRIMARY KEY,
  property_id INTEGER REFERENCES properties(id),
  tenant_name TEXT,
  status TEXT NOT NULL,              -- 'notice_sent', 'filed', 'hearing_scheduled', 'hearing_complete', 'execution'
  notice_date DATE,
  filing_date DATE,
  hearing_date DATE,
  execution_date DATE,
  jp_court TEXT,                     -- Which court
  case_number TEXT,
  assigned_to TEXT,                  -- 'Jessica' or 'Christian'
  notes TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

---

## COMMON QUERIES

### Get Properties with Mortgages
```javascript
const { data } = await supabaseClient
  .from('properties')
  .select('id, name, mortgage_lender, loan_servicer, mortgage_payment, mortgage_balance')
  .eq('active', true)
  .not('mortgage_balance', 'is', null)
  .gt('mortgage_balance', 0)
  .order('name');
```

### Get Property by Name
```javascript
const { data } = await supabaseClient
  .from('properties')
  .select('*')
  .eq('name', 'Oak Creek')
  .single();
```

### Update Property
```javascript
const { data, error } = await supabaseClient
  .from('properties')
  .update({ 
    occupancy_status: 'Vacant',
    updated_at: new Date().toISOString()
  })
  .eq('id', propertyId);
```

### Insert with Returning Data
```javascript
const { data, error } = await supabaseClient
  .from('bills')
  .insert([{
    property_id: 1,
    bill_type: 'mortgage',
    vendor: 'Texas Trust CU',
    amount: 1250.00,
    due_day: 15
  }])
  .select();  // Returns the inserted row
```

### Upsert (Insert or Update)
```javascript
const { data, error } = await supabaseClient
  .from('properties')
  .upsert({
    name: 'Oak Creek',
    zillow_value: 285000
  }, { onConflict: 'name' });
```

### Filter with Multiple Conditions
```javascript
const { data } = await supabaseClient
  .from('bill_payments')
  .select('*')
  .eq('status', 'pending')
  .lte('due_date', '2025-12-01')
  .order('due_date');
```

### Join Tables
```javascript
const { data } = await supabaseClient
  .from('bills')
  .select(`
    *,
    properties (name, full_address)
  `)
  .eq('bill_type', 'mortgage');
```

---

## INDEXES (CREATE AS NEEDED)

```sql
-- For bill tracking
CREATE INDEX idx_bills_property ON bills(property_id);
CREATE INDEX idx_bills_type ON bills(bill_type);
CREATE INDEX idx_bill_payments_status ON bill_payments(status);
CREATE INDEX idx_bill_payments_due_date ON bill_payments(due_date);

-- For evictions
CREATE INDEX idx_evictions_property ON evictions(property_id);
CREATE INDEX idx_evictions_status ON evictions(status);
```

---

## TROUBLESHOOTING

### "permission denied for table X"
```sql
-- Run this in SQL Editor
ALTER TABLE table_name DISABLE ROW LEVEL SECURITY;
```

### "column X does not exist"
- Check column name spelling (case-sensitive)
- Run your CREATE TABLE or ALTER TABLE statement
- Refresh Supabase Table Editor to verify

### "duplicate key value violates unique constraint"
- You're trying to insert a duplicate value in a UNIQUE column
- Check if record already exists before inserting
- Use UPSERT instead of INSERT

### "null value in column X violates not-null constraint"
- You're missing a required field
- Either provide the value or make the column nullable:
```sql
ALTER TABLE table_name ALTER COLUMN column_name DROP NOT NULL;
```

---

## NAMING CONVENTIONS

### Tables
- Lowercase, plural: `properties`, `bills`, `evictions`
- Use underscores: `bill_payments`, `pl_transactions`

### Columns
- Lowercase, underscores: `due_date`, `property_id`, `created_at`
- Foreign keys: `property_id` (table_id format)
- Booleans: `is_active`, `has_mortgage`, `active`
- Timestamps: `created_at`, `updated_at`, `paid_date`

### Status Values
- Lowercase, underscores: `pending`, `paid`, `overdue`, `notice_sent`
- Keep consistent across apps

---

## MIGRATION NOTES

### From Google Sheets
1. Export Google Sheet to CSV
2. Clean data in Excel (fix dates, numbers)
3. Import via Supabase Table Editor (CSV import)
4. OR write INSERT statements and run in SQL Editor

### From ClickUp
1. Export ClickUp to CSV
2. Map columns to properties table columns
3. Transform data (parse dates, currencies)
4. Insert via SQL or CSV import

---

*Reference this playbook when designing database schemas*
