# TEAM MEMBERS
**AJ Real Estate Group**
**Last Updated:** November 26, 2025

---

## ACTIVE TEAM

### Owners

| Name | Role | Card Last 4 | Primary Duties | AI Tools |
|------|------|-------------|----------------|----------|
| **JR Gramstad** | CFO & Co-Owner | ? | Acquisitions, finance, software, back office | Claude, Claude Code |
| **Ashley Gramstad** | CEO & Co-Owner | 5757 | Vision, people management, field oversight | - |

### Office Staff

| Name | Role | Card Last 4 | Primary Duties | Apps They Use |
|------|------|-------------|----------------|---------------|
| **Jessica** | Back Office Admin | 8622 | Bill paying, tenant service, eviction paperwork | Master Property Data, Bill Tracking, Credit Card Transactions |
| **Christian Rojas** | Operations Coordinator | 3891 | Maintenance tickets, vendor mgmt, inspections, eviction execution | Daily Check-ins, Inspection App |
| **Tom Tolbert** | Project Manager | 6101 | Site visits, project timelines, budgets | Daily Check-ins |

### Field Crew

| Name | Role | Card Last 4 | Status | Notes |
|------|------|-------------|--------|-------|
| **Ryder Holliman** | Crew Leader | 0000 | ✅ Good | Young, stepping up, leading crew well |
| **Jose** | Crew Leader | 0000 | ✅ Good | Stepped up, running crew alongside Ryder |
| **Omar Martinez** | Skilled Worker | 0000 | ⚠️ Unreliable | Best skills BUT moonlighting, lots of time off |

---

## FORMER TEAM (Do Not Include in Apps)

| Name | Former Role | Left | Reason |
|------|-------------|------|--------|
| **Kalen Bates** | Property Manager | Nov 2025 | FIRED - Not paying bills reliably |
| **Elijah** | Staff | 2024 | Left |
| **Becca** | Staff | 2024 | Left |

---

## FOR DROPDOWN MENUS

### "Assigned To" Options
```javascript
const assigneeOptions = [
  'Jessica',
  'Christian',
  'Tom',
  'Ryder',
  'Jose',
  'JR',
  'Ashley'
];
```

### "Paid By" / "Confirmed By" Options
```javascript
const confirmedByOptions = [
  'Jessica',
  'JR',
  'Ashley'
];
```

### "Cardholder" Options (for transactions)
```javascript
const cardholderOptions = [
  { name: 'Ashley Gramstad', card: '5757', role: 'Owner' },
  { name: 'Jessica', card: '8622', role: 'Back Office' },
  { name: 'Thomas Tolbert', card: '6101', role: 'Project Manager' },
  { name: 'Christian Rojas', card: '3891', role: 'Operations' },
  { name: 'Ryder Holliman', card: '0000', role: 'Crew Leader' },
  { name: 'Jose', card: '0000', role: 'Crew Leader' },
  { name: 'Omar Martinez', card: '0000', role: 'Maintenance' }
];
```

---

## CONTACT PREFERENCES

| Person | Primary Contact | Response Time | Best For |
|--------|-----------------|---------------|----------|
| JR | iMessage | Quick | Decisions, approvals, software |
| Ashley | iMessage | Varies | People issues, field crew, vision |
| Jessica | iMessage | Same day | Back office, bills, admin |
| Christian | iMessage | Same day | Maintenance, field ops, Spanish translation |
| Tom | iMessage | Same day | Projects, renovations, timelines |

---

## TEAM DYNAMICS (Important)

### ⚠️ Keep Separated
- **Christian + Tom** = Personality conflicts
- Assign to different properties when possible
- Don't put on same project simultaneously

### ✅ Works Well Together
- **Ryder + Jose** = Good crew leadership team
- **Jessica + JR** = Smooth back office coordination

### 📈 Succession Candidates
1. **Jessica** - HIGH potential, future Head of Back Office
2. **Christian** - HIGH potential IF interpersonal issues resolve

### 🚫 Not Succession Candidates
- **Tom** - Good PM but not leadership track

---

## SUPABASE: cardholders TABLE

```sql
-- Current data in cardholders table
SELECT * FROM cardholders WHERE active = true;

-- Expected records:
id | full_name        | card_last_4 | role            | active
---|------------------|-------------|-----------------|-------
1  | Ashley Gramstad  | 5757        | Owner           | true
2  | Jessica          | 8622        | Back Office     | true
3  | Thomas Tolbert   | 6101        | Project Manager | true
4  | Christian Rojas  | 3891        | Operations      | true
5  | Ryder Holliman   | 0000        | Crew Leader     | true
6  | Jose             | 0000        | Crew Leader     | true
7  | Omar Martinez    | 0000        | Maintenance     | true
```

---

## FUTURE HIRE (Planned)

| Field | Value |
|-------|-------|
| Position | Entry-level assistant |
| Background | Finance, AI, data science |
| Requirement | Must be AI-native |
| Timeline | When cash flow stabilizes |

---

*This file is reference material for Claude Code sessions*
