# AJ Real Estate - Claude Code Instructions
## READ THIS FIRST - Every Session

---

## Tech Stack (NON-NEGOTIABLE)

| Component | Tool | Notes |
|-----------|------|-------|
| Database | Supabase (PostgreSQL) | ONE database for all apps |
| Frontend | Vanilla JavaScript + HTML/CSS | No frameworks |
| Hosting | Netlify | Auto-deploy from GitHub |
| Development | Claude Code | You are here |

### ❌ NEVER USE
- Google Sheets as database
- Google Apps Script
- Any framework (React, Vue, etc.) unless explicitly requested

---

## Supabase Credentials

**Project:** AJ Real Estate System  
**URL:** `https://gcuunlxfgtnppnqkikaz.supabase.co`  
**Anon Key:** `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImdjdXVubHhmZ3RucHBucWtpa2F6Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjE1NzY3MTgsImV4cCI6MjA3NzE1MjcxOH0.8uKySCjd_f8sqOtYAyD2_MyvQIC_2IsYkHE1NoqtQT4`

**RLS:** Disable Row Level Security on all tables for anonymous access:
```sql
ALTER TABLE [table_name] DISABLE ROW LEVEL SECURITY;
```

---

## Shared Tables (REUSE - Never Recreate)

These tables exist and are used by multiple apps:

### properties
```sql
-- 75+ active properties, shared across ALL apps
id, name (unique), active, sort_order, created_at
-- Plus 60+ extended fields (see Property Master app)
```

### categories
```sql
-- Expense/transaction categories
id, name (unique), active, sort_order, created_at
```

### cardholders
```sql
-- Team members (for assignments, transactions, etc.)
id, full_name, card_last_4, role, active, created_at
```

**ALWAYS check if a table exists before creating. ALWAYS reuse shared tables.**

---

## Development Rules

### Rule 1: NEVER DEFER BUGS
- Bug found → Stop everything → Fix immediately
- Do not continue feature work until bug is resolved
- Do not add bugs to "fix later" list
- This is JR's #1 non-negotiable rule

### Rule 2: NO FEATURE CREEP
- Build Phase 1 ONLY as specified
- If JR suggests additions mid-build, CHALLENGE:
  - "Is this Phase 1 or Phase 2?"
  - "Should we add this to the parking lot?"
  - "Will this delay deployment?"
- Only proceed with additions if JR says "do it anyway"

### Rule 3: SPEC BEFORE CODE
- Confirm requirements before writing code
- Ask clarifying questions upfront
- Document what you're building before building it

### Rule 4: SOFT LAUNCH PHILOSOPHY
- Deploy basic version first
- Get real user feedback
- Iterate based on actual usage
- Don't wait for perfection

---

## Standard File Structure

```
project-root/
├── docs/
│   └── CLAUDE_CODE_INSTRUCTIONS.md   ← This file
├── frontend/
│   ├── index.html
│   ├── app.js
│   ├── styles.css
│   └── config.js                      ← Supabase credentials
├── database/
│   └── schema.sql                     ← Table definitions
└── README.md
```

---

## Standard config.js Template

```javascript
const config = {
  supabase: {
    url: 'https://gcuunlxfgtnppnqkikaz.supabase.co',
    anonKey: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImdjdXVubHhmZ3RucHBucWtpa2F6Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjE1NzY3MTgsImV4cCI6MjA3NzE1MjcxOH0.8uKySCjd_f8sqOtYAyD2_MyvQIC_2IsYkHE1NoqtQT4'
  }
};
```

---

## Standard Supabase Client Setup

### In HTML (add to `<head>`)
```html
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
```

### In JavaScript (app.js)
```javascript
const supabaseClient = supabase.createClient(
  config.supabase.url, 
  config.supabase.anonKey
);
```

---

## Communication Style with JR

- **Bottom line first**, then details
- **Challenge ideas** when appropriate - JR wants pushback
- **Execute immediately** when JR says "do it anyway"
- **Be concise** - JR moves fast
- **State decision level** when relevant (Level 1/2/3)

---

## Decision Framework Reference

| Level | Timeline | Example |
|-------|----------|---------|
| Level 1 | Instant (<5 min) | Fix bug, approve standard pattern |
| Level 2 | 10-15 minutes | New feature scope, architectural choice |
| Level 3 | 2+ weeks | Major system changes, new app decisions |

---

## Current App Context

**[FILL IN PER PROJECT]**

### App Name: [Name]

### Purpose: 
[What this app does]

### Primary User:
[Who uses it - Jessica, Christian, Kalen, Tom, JR]

### Current Phase:
[What we're building now]

### Phase 2 Parking Lot (DO NOT BUILD):
- [Future feature 1]
- [Future feature 2]

### App-Specific Tables:
- [table_name] - [purpose]

---

## Before Starting Any Work

1. Confirm you've read this file
2. State what you understand the task to be
3. Ask any clarifying questions
4. Get JR's approval before writing code

---

## Troubleshooting Checklist

### Data not showing in app:
1. ✅ Check RLS is disabled
2. ✅ Verify config.js has correct Supabase URL
3. ✅ Check browser console for errors
4. ✅ Test query directly: `supabaseClient.from('table').select('*').limit(5)`

### Deployment not updating:
1. ✅ Verify GitHub push succeeded
2. ✅ Check Netlify deploy status
3. ✅ Hard refresh browser (Ctrl+Shift+R)

---

*Last Updated: November 2025*
*Owner: JR, AJ Real Estate Group*
