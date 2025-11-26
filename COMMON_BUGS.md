# COMMON BUGS & FIXES
**AJ Real Estate Group - Development Reference**
**Last Updated:** November 26, 2025

---

## SUPABASE ISSUES

### ❌ "permission denied for table X"

**Symptom:** App loads but shows no data, or errors on save

**Cause:** Row Level Security (RLS) is enabled

**Fix:**
```sql
ALTER TABLE table_name DISABLE ROW LEVEL SECURITY;
```

**Prevention:** Always run this after creating any new table

---

### ❌ "column X does not exist"

**Symptom:** Query fails, console shows column not found

**Cause:** Table schema doesn't match code

**Fix:**
1. Check column name spelling (case-sensitive!)
2. Run ALTER TABLE to add missing column:
```sql
ALTER TABLE table_name ADD COLUMN column_name TEXT;
```
3. Or verify CREATE TABLE was run

**Prevention:** Always run schema.sql before testing app

---

### ❌ "null value violates not-null constraint"

**Symptom:** Insert/update fails

**Cause:** Required field is missing

**Fix Options:**
1. Provide the value in code
2. Make column nullable:
```sql
ALTER TABLE table_name ALTER COLUMN column_name DROP NOT NULL;
```

**Prevention:** Avoid NOT NULL constraints during development (JR's rule: no required fields that block data entry)

---

### ❌ "duplicate key value violates unique constraint"

**Symptom:** Insert fails on duplicate

**Cause:** Trying to insert duplicate value in UNIQUE column

**Fix:**
1. Check if record exists before inserting
2. Use UPSERT instead:
```javascript
const { data, error } = await supabaseClient
  .from('table_name')
  .upsert({ ... }, { onConflict: 'unique_column' });
```

---

### ❌ Data shows in Supabase but not in app

**Symptom:** Table Editor shows records, app shows empty

**Checklist:**
1. ✅ RLS disabled?
2. ✅ config.js has correct project URL?
3. ✅ anon key is correct?
4. ✅ Query has correct table name?
5. ✅ Filters not excluding all records?

**Debug:**
```javascript
// Test in browser console
const { data, error } = await supabaseClient
  .from('table_name')
  .select('*')
  .limit(5);
console.log({ data, error });
```

---

## NETLIFY / DEPLOYMENT ISSUES

### ❌ Changes not showing after deploy

**Symptom:** Code pushed but app shows old version

**Checklist:**
1. ✅ GitHub push went through? (check repo)
2. ✅ Netlify build triggered? (check Deploys tab)
3. ✅ Build succeeded? (check logs)
4. ✅ Browser cache cleared?

**Fix:**
1. Hard refresh: `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)
2. Open in incognito window
3. Check Netlify deploy logs for errors

---

### ❌ Netlify build failed

**Symptom:** Deploy shows "Failed" in Netlify

**Common Causes:**
1. Syntax error in JavaScript
2. Missing file referenced in HTML
3. Wrong publish directory

**Fix:**
1. Check Netlify build logs (shows exact error)
2. Fix the error in code
3. Push again

---

### ❌ 404 on page refresh (React apps)

**Symptom:** Direct URL or refresh returns 404

**Cause:** React Router needs redirect rules

**Fix:** Add `_redirects` file to public folder:
```
/*    /index.html   200
```

---

## JAVASCRIPT / FRONTEND ISSUES

### ❌ "supabaseClient is not defined"

**Symptom:** App crashes on load

**Cause:** Supabase client not initialized or script load order wrong

**Fix:**
1. Check script order in HTML (Supabase CDN must load first):
```html
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<script src="config.js"></script>
<script src="app.js"></script>
```

2. Verify client initialization:
```javascript
const supabaseClient = supabase.createClient(
  config.supabase.url,
  config.supabase.anonKey
);
```

---

### ❌ "config is not defined"

**Symptom:** App can't find Supabase credentials

**Cause:** config.js not loaded or wrong path

**Fix:**
1. Verify config.js exists
2. Check script tag path is correct
3. Check config.js syntax (valid JavaScript object)

---

### ❌ Async/await not working

**Symptom:** Data undefined, promise not resolved

**Cause:** Missing await or function not async

**Fix:**
```javascript
// Wrong
function loadData() {
  const { data } = supabaseClient.from('table').select('*');
  console.log(data); // undefined!
}

// Correct
async function loadData() {
  const { data } = await supabaseClient.from('table').select('*');
  console.log(data); // actual data
}
```

---

### ❌ Event listener not firing

**Symptom:** Button click does nothing

**Cause:** Element doesn't exist when listener attached

**Fix:**
```javascript
// Wait for DOM to load
document.addEventListener('DOMContentLoaded', () => {
  document.getElementById('myButton').addEventListener('click', handleClick);
});
```

---

## DATA ISSUES

### ❌ Dates displaying wrong

**Symptom:** Date shows as wrong day or weird format

**Cause:** Timezone conversion issues

**Fix:**
```javascript
// When saving to Supabase (store as date only, no time)
const dateValue = '2025-11-26'; // YYYY-MM-DD format

// When displaying
const date = new Date(dateValue + 'T00:00:00'); // Force local timezone
const display = date.toLocaleDateString(); // MM/DD/YYYY
```

---

### ❌ Numbers showing as strings

**Symptom:** Math operations fail, sorting wrong

**Cause:** Data came in as string

**Fix:**
```javascript
const amount = parseFloat(data.amount) || 0;
const count = parseInt(data.count) || 0;
```

---

### ❌ Empty strings vs null

**Symptom:** Filters not working as expected

**Cause:** Column has '' (empty string) instead of null

**Fix for queries:**
```javascript
// Check both null and empty
.or('property.is.null,property.eq.""')
```

---

## GOOGLE SHEETS LEGACY ISSUES

### ❌ CORS errors

**Symptom:** API call blocked by browser

**Cause:** Google Sheets API doesn't allow browser requests

**Fix:** DON'T USE GOOGLE SHEETS. Migrate to Supabase.

---

## QUICK DEBUG CHECKLIST

When something doesn't work:

1. [ ] Open browser console (F12) - any errors?
2. [ ] Check Network tab - API calls failing?
3. [ ] Check Supabase Table Editor - data exists?
4. [ ] Check RLS is disabled on all tables
5. [ ] Check config.js has correct credentials
6. [ ] Hard refresh browser (Ctrl+Shift+R)
7. [ ] Check Netlify deploy status
8. [ ] Test query directly in console

---

## JR'S BUG RULE

**NEVER DEFER BUGS**

When you find a bug:
1. STOP feature work
2. Fix the bug immediately
3. Test the fix
4. Then continue

No exceptions. No "fix later." No Phase 2.

---

*Add new bugs and fixes to this file as discovered*
