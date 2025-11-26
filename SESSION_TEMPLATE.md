# SESSION NOTES TEMPLATE
**Use this at end of every Claude Code session**

---

## Instructions

At the end of each Claude Code session, ask:

```
Generate session notes using this format. I'll save them for the next session.
```

Then save the output to a file like `SESSION_2025-11-26.md` in your repo or notes.

---

## Template

```markdown
# SESSION NOTES
**Date:** [DATE]
**App:** [APP NAME]
**Duration:** [APPROX TIME]

---

## WHAT WAS BUILT

- [Feature 1]
- [Feature 2]
- [Feature 3]

---

## WHAT'S WORKING

✅ [Working feature 1]
✅ [Working feature 2]
✅ [Working feature 3]

---

## WHAT'S LEFT TO DO

- [ ] [Remaining task 1]
- [ ] [Remaining task 2]
- [ ] [Remaining task 3]

---

## BUGS FOUND / FIXED

| Bug | Status | Fix |
|-----|--------|-----|
| [Bug description] | ✅ Fixed | [How it was fixed] |
| [Bug description] | 🔴 Open | [Notes] |

---

## FILES CHANGED

- `path/to/file1.js` - [what changed]
- `path/to/file2.html` - [what changed]
- `database/schema.sql` - [what changed]

---

## DATABASE CHANGES

```sql
-- Tables created/modified
[SQL statements run]
```

---

## DEPLOYMENT STATUS

| Environment | Status | URL |
|-------------|--------|-----|
| Netlify | ✅ Deployed | [URL] |
| Supabase | ✅ Schema updated | [Dashboard link] |

---

## NEXT SESSION SHOULD

1. [First priority for next session]
2. [Second priority]
3. [Third priority]

---

## QUESTIONS / DECISIONS NEEDED

- [Any open questions for JR]
- [Decisions that need to be made]

---

## CONTEXT FOR NEXT SESSION

[Any important context the next Claude Code session should know]

```

---

## Example Filled Out

```markdown
# SESSION NOTES
**Date:** November 26, 2025
**App:** Bill Tracking System
**Duration:** ~2 hours

---

## WHAT WAS BUILT

- Database schema (bills, bill_payments tables)
- Basic UI structure (dashboard, add bill form, payment tracking)
- Property dropdown populated from Supabase
- Monthly bill generation logic

---

## WHAT'S WORKING

✅ Bills table created in Supabase
✅ Property dropdown loads from properties table
✅ Can add new bill records
✅ Dashboard shows counts (due/paid/overdue)

---

## WHAT'S LEFT TO DO

- [ ] Payment confirmation workflow
- [ ] Color coding (red/yellow) for alerts
- [ ] Due date filtering
- [ ] CSV export
- [ ] Load 46 mortgages data

---

## BUGS FOUND / FIXED

| Bug | Status | Fix |
|-----|--------|-----|
| RLS blocking reads | ✅ Fixed | Disabled RLS on bills table |
| Date picker wrong format | ✅ Fixed | Changed to YYYY-MM-DD |
| Property dropdown empty | 🔴 Open | Need to check query |

---

## FILES CHANGED

- `frontend/index.html` - Added dashboard and forms
- `frontend/app.js` - Core logic, Supabase queries
- `frontend/styles.css` - Basic styling
- `database/schema.sql` - bills and bill_payments tables

---

## DATABASE CHANGES

```sql
CREATE TABLE bills (...);
CREATE TABLE bill_payments (...);
ALTER TABLE bills DISABLE ROW LEVEL SECURITY;
ALTER TABLE bill_payments DISABLE ROW LEVEL SECURITY;
```

---

## DEPLOYMENT STATUS

| Environment | Status | URL |
|-------------|--------|-----|
| Netlify | ✅ Deployed | https://aj-bill-tracking.netlify.app |
| Supabase | ✅ Schema updated | Dashboard |

---

## NEXT SESSION SHOULD

1. Fix property dropdown bug
2. Complete payment confirmation flow
3. Add color coding alerts
4. Test with real mortgage data

---

## QUESTIONS / DECISIONS NEEDED

- Should "paid" status auto-set when checkbox clicked, or require explicit save?
- Do we need an "undo payment" feature?

---

## CONTEXT FOR NEXT SESSION

Bill Tracking Phase 1 is 60% complete. Core structure working. Need to finish payment workflow and add alert colors before user testing with Jessica.
```

---

*Save session notes to track progress across Claude Code sessions*
