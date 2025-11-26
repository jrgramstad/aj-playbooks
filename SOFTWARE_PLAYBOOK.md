# SOFTWARE DEVELOPMENT PLAYBOOK
**For Claude Code Sessions**
**Last Updated:** November 26, 2025

---

## CRITICAL RULES (NON-NEGOTIABLE)

### 1. NEVER DEFER BUGS
```
Bug found → STOP everything → Fix immediately → Test → Continue
```
No exceptions. No "fix later." No "Phase 2." Fix NOW.

### 2. NO FEATURE CREEP
When JR suggests adding features mid-build:
- Challenge: "Is this Phase 1 or Phase 2?"
- If Phase 2 → Document in parking lot, don't build
- If JR says "do it anyway" → Execute immediately

### 3. SPEC BEFORE CODE
Never start coding without confirming:
- What problem are we solving?
- Who is the user?
- What's the minimum viable Phase 1?
- What's explicitly NOT in scope?

### 4. SOFT LAUNCH PHILOSOPHY
- Deploy basic working version first
- Get real user feedback
- Iterate based on actual usage
- Don't wait for "perfect"

---

## STANDARD TECH STACK

| Component | Tool | Notes |
|-----------|------|-------|
| **Database** | Supabase (PostgreSQL) | ONE database for all apps |
| **Frontend** | Vanilla JS + HTML/CSS | No React/Vue unless requested |
| **Hosting** | Netlify | Auto-deploy from GitHub |
| **Development** | Claude Code | All coding here |

### ❌ NEVER USE
- Google Sheets as database
- Google Apps Script
- ClickUp
- Complex frameworks (unless specifically requested)

---

## BUILD WORKFLOW

### Phase 1: Specification (WITH JR)
1. Define the problem (one sentence)
2. Identify the user (who uses this daily?)
3. List Phase 1 features (minimum viable)
4. Create Phase 2 parking lot (ideas for later)
5. Define success criteria

**Output:** Clear spec before ANY code

### Phase 2: Database Design
1. Check SUPABASE_STANDARD.md for existing tables
2. Reuse shared tables: `properties`, `categories`, `cardholders`
3. Design new tables only if needed
4. Run schema in Supabase SQL Editor

**Output:** Tables ready in Supabase

### Phase 3: Build Frontend
1. Create index.html with structure
2. Create app.js with logic
3. Create styles.css for styling
4. Create config.js with Supabase credentials
5. Test locally if possible

**Output:** Working frontend files

### Phase 4: Deploy
1. Push to GitHub (Claude Code does this)
2. Connect repo to Netlify
3. Deploy automatically
4. Test live URL

**Output:** Live app URL

### Phase 5: User Training
1. 5-minute walkthrough with user
2. Watch them use it once
3. Note friction points
4. Document for iteration

**Output:** User actively using app

---

## FILE STRUCTURE (STANDARD)

```
/app-name/
├── frontend/
│   ├── index.html      # Main HTML
│   ├── app.js          # All JavaScript
│   ├── styles.css      # All CSS
│   └── config.js       # Supabase credentials
├── database/
│   └── schema.sql      # Table definitions
└── README.md           # App documentation
```

---

## SUPABASE PATTERNS

### Standard Config (config.js)
```javascript
const config = {
  supabase: {
    url: 'https://gcuunlxfgtnppnqkikaz.supabase.co',
    anonKey: '[GET FROM SUPABASE_STANDARD.md]'
  }
};
```

### Initialize Client (app.js)
```javascript
const supabaseClient = supabase.createClient(
  config.supabase.url,
  config.supabase.anonKey
);
```

### Common Queries
```javascript
// SELECT all
const { data, error } = await supabaseClient
  .from('table_name')
  .select('*')
  .order('created_at', { ascending: false });

// SELECT with filter
const { data, error } = await supabaseClient
  .from('properties')
  .select('*')
  .eq('active', true);

// INSERT
const { data, error } = await supabaseClient
  .from('table_name')
  .insert([{ column1: 'value1', column2: 'value2' }]);

// UPDATE
const { data, error } = await supabaseClient
  .from('table_name')
  .update({ column1: 'new_value' })
  .eq('id', recordId);

// DELETE
const { data, error } = await supabaseClient
  .from('table_name')
  .delete()
  .eq('id', recordId);
```

### Always Disable RLS
```sql
ALTER TABLE table_name DISABLE ROW LEVEL SECURITY;
```

---

## UI/UX STANDARDS

### For Office Users (Jessica)
- Desktop-first design
- Clear labels
- Tables with sorting
- Export to CSV
- Confirmation dialogs for destructive actions

### For Field Users (Christian/Tom)
- Mobile-first design
- BIG buttons (easy to tap)
- Minimal typing required
- Dropdowns over text fields
- Works offline if possible

### Universal Rules
- No required fields unless truly required
- Auto-save when possible
- Clear error messages
- Loading indicators for async operations
- Color coding: Green=good, Yellow=warning, Red=bad

---

## DECISION FRAMEWORK FOR DEVELOPMENT

### Level 1 (Instant - Just Do It)
- Fix any bug
- Add missing error handling
- Improve UI clarity
- Fix typos or labels

### Level 2 (Ask JR - 10 min discussion)
- Add new feature to existing app
- Change data structure
- Add new table
- Change user workflow

### Level 3 (Requires Spec)
- Build new app
- Major architecture change
- Integration with external system

---

## COMMON ISSUES & FIXES

### "Data not showing"
1. Check RLS is disabled: `ALTER TABLE x DISABLE ROW LEVEL SECURITY;`
2. Check config.js has correct Supabase URL
3. Check browser console for errors
4. Verify data exists in Supabase Table Editor

### "Can't connect to Supabase"
1. Verify anon key is correct
2. Check Supabase project is active
3. Test query in Supabase SQL Editor first

### "Netlify not updating"
1. Check GitHub push went through
2. Check Netlify build logs
3. Hard refresh browser (Ctrl+Shift+R)
4. Clear browser cache

---

## APP PRIORITIES (November 2025)

| Priority | App | Status | User |
|----------|-----|--------|------|
| #1 | Bill Tracking | Building NOW | Jessica |
| #2 | ClickUp CSV Import | Next | JR |
| #3 | Eviction Tracking | After #2 | Jessica/Christian |
| #4 | Daily Check-ins | After #3 | Christian/Tom |

### On Hold
- Auction Prep (no auctions 1-2 months)
- P&L App (manual for now)
- Project Command Center

---

## QUICK CHECKLIST FOR NEW APPS

Before starting:
- [ ] Problem clearly defined
- [ ] User identified
- [ ] Phase 1 scope agreed
- [ ] Shared tables identified (properties, categories, cardholders)
- [ ] New tables designed (if any)

Before deploying:
- [ ] RLS disabled on all tables
- [ ] Error handling in place
- [ ] Works on target device (desktop/mobile)
- [ ] No required fields blocking data entry
- [ ] User can complete core workflow

After deploying:
- [ ] User trained (5 min walkthrough)
- [ ] User can use independently
- [ ] Bugs fixed same day
- [ ] Phase 2 parking lot documented

---

*Reference this playbook at start of every Claude Code session*
