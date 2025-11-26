# APP INVENTORY
**AJ Real Estate Group - All Applications**
**Last Updated:** November 26, 2025

---

## ACTIVE APPS

### ✅ Master Property Data
| Field | Value |
|-------|-------|
| **Status** | Deployed, needs data population |
| **URL** | [Add Netlify URL] |
| **Repo** | [Add GitHub repo] |
| **Stack** | React + Supabase |
| **User** | Jessica, JR |
| **Purpose** | Central property database - foundation for all apps |
| **Priority** | #2 - Import ClickUp CSV |

**Key Tables:** `properties` (77 records)

**Notes:**
- 77 properties loaded but data is sparse
- Need to import from ClickUp CSV to populate fields
- Remove required fields that block data entry

---

### ✅ Bill Tracking (Building Now)
| Field | Value |
|-------|-------|
| **Status** | 🔨 In Development |
| **URL** | [TBD] |
| **Repo** | [TBD] |
| **Stack** | Vanilla JS + Supabase |
| **User** | Jessica |
| **Purpose** | Track mortgage payments, prevent missed bills |
| **Priority** | #1 - CRITICAL |

**Key Tables:** `bills`, `bill_payments`

**Phase 1 Scope:**
- 46 mortgages only
- Monthly bill generation
- Payment confirmation (checkbox + date + who)
- Dashboard: Due/Paid/Overdue
- Visual alerts: Red (overdue), Yellow (≤5 days)

---

### ✅ Rent or Flip Tool
| Field | Value |
|-------|-------|
| **Status** | Working |
| **URL** | [Add URL] |
| **Stack** | Vanilla JS |
| **User** | JR |
| **Purpose** | Decision tool: rent vs. sell analysis |
| **Priority** | Keep as-is |

**Notes:** Standalone tool, working well, no changes needed.

---

## NEEDS WORK

### 🔄 Credit Card Transactions
| Field | Value |
|-------|-------|
| **Status** | Stale - needs refresh |
| **URL** | [Add URL if deployed] |
| **Stack** | Vanilla JS + Supabase |
| **User** | Jessica |
| **Purpose** | Process daily CC transactions |
| **Priority** | Later - after Bill Tracking stable |

**Key Tables:** `transactions`, `categories`, `cardholders`, `properties`

---

### 🔄 Property Inspection App
| Field | Value |
|-------|-------|
| **Status** | Not used - too complex |
| **URL** | [Add URL if deployed] |
| **Stack** | Vanilla JS + Supabase |
| **User** | Christian |
| **Purpose** | Digital property inspections |
| **Priority** | Later - needs simplification |

**Key Tables:** `inspections`, `inspection_items`

---

## NOT BUILT YET

### 📋 Eviction Tracking
| Field | Value |
|-------|-------|
| **Status** | Not built |
| **Stack** | Vanilla JS + Supabase |
| **User** | Jessica (paperwork), Christian (execution) |
| **Purpose** | Track eviction status and key dates |
| **Priority** | #3 |

**Proposed Tables:** `evictions`

**Planned Features:**
- Link to property
- Status stages: Notice → Filed → Hearing → Execution
- Assigned to Jessica or Christian
- JP Court field
- Key dates tracking

---

### 📋 Daily Check-in Forms
| Field | Value |
|-------|-------|
| **Status** | Not built |
| **Stack** | Vanilla JS + Supabase |
| **User** | Christian, Tom |
| **Purpose** | Simple daily journal from field |
| **Priority** | #4 |

**Proposed Tables:** `daily_checkins`

**Planned Features:**
- Property dropdown
- Scale 1-10: How did today go?
- What went right/wrong (short text)
- Any blockers? (yes/no)
- Big buttons, mobile-friendly

---

## ON HOLD / PAUSED

### ⏸️ Auction Prep Software
| Field | Value |
|-------|-------|
| **Status** | Paused |
| **Reason** | No auctions for 1-2 months (cash flow) |
| **Resume** | When auctions resume |

---

### ⏸️ P&L App
| Field | Value |
|-------|-------|
| **Status** | Paused |
| **Reason** | JR can do manually at tax time |
| **Resume** | After core ops stable |

---

### ⏸️ Project Command Center
| Field | Value |
|-------|-------|
| **Status** | Paused |
| **Reason** | Core ops apps take priority |
| **Resume** | After Bill Tracking, Evictions, Check-ins working |

---

### ⏸️ MCP Server / AI Intelligence
| Field | Value |
|-------|-------|
| **Status** | Paused |
| **Reason** | Need operations streamlined first |
| **Resume** | Phase 2 after core apps stable |

---

## ABANDONED

### 🗑️ P&L Legacy (Google Sheets)
- **Reason:** Start fresh in Supabase
- **Action:** Do not resurrect

### 🗑️ Balance Sheet (Google Sheets)
- **Reason:** Start fresh in Supabase
- **Action:** Do not resurrect

### 🗑️ Property Portal
- **Reason:** Replaced by ChatGPT custom GPTs
- **Action:** Do not resurrect

### 🗑️ Project Tracker
- **Reason:** Using Apple Reminders instead
- **Action:** Do not resurrect

---

## NETLIFY SITES

| App | Netlify URL | Status |
|-----|-------------|--------|
| Master Property Data | [Add] | ✅ |
| Bill Tracking | [Add when deployed] | 🔨 |
| Credit Card Transactions | [Add] | ⏸️ |
| Rent or Flip | [Add] | ✅ |

---

## GITHUB REPOS

| Repo | Purpose | Status |
|------|---------|--------|
| aj-playbooks | Standards, playbooks, context docs | ✅ Active |
| [master-property-data] | Master Property Data app | ✅ |
| [bill-tracking] | Bill Tracking app | 🔨 Building |
| [other repos...] | [Add as needed] | |

---

## SUPABASE TABLES OVERVIEW

### Shared Tables (Used by Multiple Apps)
| Table | Records | Used By |
|-------|---------|---------|
| `properties` | 77 | All apps |
| `categories` | ~15 | Credit Card, P&L |
| `cardholders` | ~8 | Credit Card, Bill Tracking |

### App-Specific Tables
| Table | App | Records |
|-------|-----|---------|
| `transactions` | Credit Card | ? |
| `pl_transactions` | P&L | ~7,600 |
| `bills` | Bill Tracking | TBD |
| `bill_payments` | Bill Tracking | TBD |
| `evictions` | Eviction Tracking | TBD |
| `daily_checkins` | Daily Check-ins | TBD |

---

## PRIORITY ORDER (November 2025)

1. **Bill Tracking** - 🔨 Building now
2. **ClickUp CSV Import** - Populate Master Property Data
3. **Eviction Tracking** - After #2
4. **Daily Check-ins** - After #3

---

*Update this file when apps are deployed or status changes*
