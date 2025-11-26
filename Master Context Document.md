# AJ Real Estate - Master Context Document
## For Claude Code Development
**Last Updated:** November 26, 2025

---

## Company Overview

| Field | Value |
|-------|-------|
| **Company** | AJ Real Estate Group |
| **Business** | 77-property rental portfolio (DFW, Texas) |
| **Method** | BRRRR (Buy, Rehab, Rent, Refinance, Repeat) + Now selling some properties |
| **Acquisition** | Monthly foreclosure auctions (Auction.com) - PAUSED 1-2 months |
| **Goal** | Scale to 100 properties, move to autopilot (90% strategic, 10% reactive) |

### Current Financial Status (Nov 2025)
- **Cash flow:** CONSTRAINED until refinance closes
- **Funding:** $1M LOC approved with Regent Bank (Samuel)
- **First refinance:** Oak Creek (McKinney) - 85-90% complete, waiting on paperwork
- **Property taxes:** Due Jan 31, 2026 (prefer to pay by Dec 31 for tax deduction)
- **Auctions:** Paused until cash flow resolved

### Property Portfolio
- **Total properties:** 77
- **Free & clear:** 31 (no mortgage)
- **With mortgages:** ~46
- **Mortgage servicers:** ~10 different companies (Texas Trust CU, various Novus transfers)

---

## Owners

### JR (CFO & Co-Owner) - PRIMARY USER
| Field | Value |
|-------|-------|
| **Role** | Acquisitions, back office, finance, software development |
| **Background** | Former CPA (sold Gramstead CPA, Tax Advisers winding down) |
| **Strengths** | Building software, analytical work, deal analysis, automation |
| **Weakness** | People management, feature creep in software |
| **Work hours** | 5 focused hours/day, peaks at 6 AM and 9:30 PM |
| **Decision style** | 80% info is enough, decide fast |
| **Current focus** | Bill tracking system, automating operations |

### Ashley (CEO & Co-Owner)
| Field | Value |
|-------|-------|
| **Role** | Vision, people management, field operations oversight |
| **Involvement** | Part-time presence |
| **Consulted on** | Strategic decisions, field crew issues |

---

## Team Structure (Updated Nov 26, 2025)

### Jessica (Back Office Admin) ⭐ KEY PERSON
| Field | Value |
|-------|-------|
| **Primary duties** | Bill paying, tenant customer service, eviction paperwork |
| **Additional** | Executive assistant tasks, winding down Tax Advisers work |
| **Apps she'll use** | Master Property Data, Bill Tracking, Credit Card Transactions |
| **Skills** | Teachable, reliable, detail-oriented |
| **Succession potential** | HIGH - future Head of Back Office |
| **AI tools** | ChatGPT for property maintenance decisions |

### Christian (Operations Coordinator) ⭐ KEY PERSON
| Field | Value |
|-------|-------|
| **Primary duties** | Maintenance tickets, troubleshooting, vendor management |
| **Field duties** | Inspections, Home Depot orders, eviction execution |
| **Split** | 50% office, 50% field |
| **Special skill** | Speaks Spanish (crucial for crew communication) |
| **Apps he'll use** | Daily check-in forms, Inspection app, Maintenance tracking |
| **Succession potential** | HIGH - if interpersonal issues resolve |
| **New responsibility** | Taking over vendor management from Kalen (cost-effective focus) |

### Tom (Project Manager)
| Field | Value |
|-------|-------|
| **Role** | Renovation project management |
| **Status** | Self-sufficient, no changes |
| **Duties** | Site visits, timelines, budgets, next plans |
| **Note** | Keep separated from Christian when possible |
| **Apps he'll use** | Daily check-in forms |
| **Succession potential** | LOW |

### Field Crew
| Person | Role | Notes |
|--------|------|-------|
| **Ryder** | Crew Leader | Young, doing good job |
| **Jose** | Crew Leader | Stepped up, running crew |
| **Omar** | Skilled Worker | Top performer BUT unreliable (moonlighting), keeping for skills |

### REMOVED
| Person | Former Role | Reason | Date |
|--------|-------------|--------|------|
| **Kalen** | Property Manager | Fired - not paying bills | Nov 2025 |

### Future Hire (Planned)
- Entry-level position
- Background: Finance, AI, or data science (college student OK)
- Must be AI-native
- Will help with data/automation side of business

---

## Critical Business Context

### The Bill Payment Crisis
**What happened:** Kalen wasn't paying bills reliably. This is existential threat.

**Solution being built:** Bill Tracking System
- Track every mortgage payment (46 mortgages)
- Confirmation that each bill was paid
- Jessica takes over all bill paying
- Start with mortgages, expand to utilities/insurance/taxes

**Payment methods:**
- Most mortgages on autopay
- Some require mailed checks (no online access)
- Due dates scattered throughout month (most due 15th)

### Property Tax Situation
- **Due:** January 31, 2026
- **Preferred:** Pay by December 31, 2025 (tax deduction)
- **Depends on:** Refinance closing and cash flow

### Selling Strategy (New)
- Now selling some properties, not just BRRRR
- **First attempt:** Primrose (Forney) - FAILED (bad micromarket + 2BR)
- **Learning:** Forney market struggling, 2BR harder to sell
- **Next:** Trying another property sale

### Evictions
- Economy bad = more evictions happening
- **Process split:**
  - Jessica: Files all paperwork
  - Christian: Attends hearings, performs physical eviction
- **Need:** Eviction tracking module (currently black box)

---

## Software Strategy

### Philosophy
> "Build one cohesive system where all apps branch off Master Property Data"

### Current Reality
- 10+ apps built in silos
- None actively used in production
- Legacy Google Sheets apps abandoned
- Moving everything to Claude Code

### Tech Stack (NON-NEGOTIABLE)
| Component | Tool |
|-----------|------|
| Database | Supabase (PostgreSQL) |
| Frontend | Vanilla JavaScript + HTML/CSS |
| Hosting | Netlify (auto-deploy from GitHub) |
| Development | Claude Code (Opus 4) |
| Team AI | ChatGPT (daily tasks) |
| Strategic AI | Claude (JR's planning/coding) |

### ❌ NEVER USE
- Google Sheets as database
- Google Apps Script
- ClickUp (abandoned - too complex)

### The Master Property Data Concept
**All apps should branch from Master Property Data as the foundation:**
```
MASTER PROPERTY DATA (77 properties)
├── Bill Tracking Module (mortgages, utilities, taxes)
├── Eviction Tracking Module
├── Daily Check-ins Module (Christian/Tom)
├── Maintenance Requests Module
├── Vendor Database Module
└── Future: P&L, Balance Sheet, KPIs
```

---

## App Status (Nov 26, 2025)

### ✅ Keep & Improve
| App | Status | Priority | Notes |
|-----|--------|----------|-------|
| **Master Property Data** | 77 properties loaded, data sparse | #2 | Foundation for everything. Need ClickUp CSV import. Remove required fields blocking data entry. |
| **Bill Tracking** | Building NOW | #1 | Start with 46 mortgages. Track payment + confirmation. |
| **Rent or Flip Tool** | Working well | Keep | Standalone decision tool, doesn't need integration |

### 🔄 Need Work
| App | Status | Priority | Notes |
|-----|--------|----------|-------|
| **Daily Check-in Forms** | Not built | #4 | Simple: 1-10 scales, yes/no, minimal text. Journal style for Christian/Tom |
| **Eviction Tracking** | Not built | #3 | Module of Master Property Data. Texas process is standardized. |
| **Credit Card Transactions** | Stale | Later | Revisit after bill tracking stable |
| **Property Inspection** | Not used | Later | Christian/Tom not using. Needs to be simpler. |

### ⏸️ Paused
| App | Reason |
|-----|--------|
| **Auction Prep** | No auctions for 1-2 months |
| **MCP Server / Claude Desktop** | Wait until operations streamlined |
| **P&L App** | Back burner - JR can do manually at tax time |
| **Balance Sheet** | Convert from Google Sheets later |

### 🗑️ Abandon
| App | Reason |
|-----|--------|
| **P&L Legacy (Google Sheets)** | Start fresh |
| **Balance Sheet (Google Sheets)** | Start fresh |
| **Property Portal** | Replaced by ChatGPT custom GPTs |
| **Project Tracker** | Using Apple Reminders instead |

---

## 30-Day Priority Roadmap

### Week 1-2: Bill Tracking System 🔴 CRITICAL
**Goal:** Never miss a mortgage payment again

**Features:**
- List of 46 mortgages with: property, lender, servicer, amount, due date
- Monthly bill generation (auto-create expected bills)
- Payment confirmation checkbox + date
- Dashboard: What's due, what's paid, what's overdue
- Jessica is primary user

**Data needed:**
- Import from ClickUp CSV (mortgage amount, servicer info)
- Manual entry for due dates, payment methods

### Week 2-3: ClickUp CSV Import
**Goal:** Populate Master Property Data without manual entry

**Import these fields:**
- Bathrooms, Bedrooms, Square footage, Year built
- Zillow value, Acquisition cost, Acquisition method, Date acquired
- Fair market rent, Traditional rent
- Interest rate, Monthly payment, Mortgage amount
- Refi Bank (originator), Servicer
- JP Court (for evictions)

**Skip these fields:**
- ClickUp metadata (task ID, comments, dates)
- Checkboxes for rooms (low value)
- Tracking numbers, space/folder info

### Week 3-4: Eviction Tracking Module
**Goal:** Make evictions visible and trackable

**Features:**
- Link to property in Master Property Data
- Status stages: Notice sent → Filed → Hearing scheduled → Hearing complete → Execution
- Assigned to: Jessica (paperwork) or Christian (field)
- JP Court (from ClickUp data)
- Key dates: Notice date, filing date, hearing date, execution date
- Notes field

### Week 4+: Daily Check-in Forms
**Goal:** Simple journal for Christian/Tom

**Features:**
- Property worked on (dropdown)
- Scale 1-10: How did today go?
- What went right? (short text)
- What went wrong? (short text)
- Any blockers? (yes/no + text if yes)
- Big buttons, minimal typing
- Mobile-friendly

---

## Data Integration Opportunities

### APIs to Explore
| Source | Data | Priority |
|--------|------|----------|
| **Zillow** | Property values, rent estimates | High |
| **DoorLoop** | Tenant info, maintenance requests | Medium |
| **ClockShark** | Crew timesheets | Low (no API) |

### Manual Imports
| Source | Data | Method |
|--------|------|--------|
| **ClickUp CSV** | Property attributes, financials | One-time import |
| **Bank statements** | Transaction history | CSV upload |

---

## Communication Style with JR

### Do This
- **Bottom line first**, then details
- **Challenge ideas** when appropriate - JR wants pushback
- **Execute immediately** when JR says "do it anyway"
- **Be concise** - JR moves fast
- **State decision level** (Level 1/2/3) when relevant
- **Automate everything possible** - JR's mantra

### Don't Do This
- Don't defer bugs or suggest deferring
- Don't build Phase 2 before Phase 1 works
- Don't add features without challenging if needed
- Don't make forms with lots of required fields (blocks data entry)
- Don't suggest Google Sheets or ClickUp

---

## Decision Framework

| Level | Time | When to Use | Example |
|-------|------|-------------|---------|
| **Level 1** | <5 min | Clear answer, low risk, done before | Fix bug, approve pattern |
| **Level 2** | 10-15 min | Needs analysis, moderate impact | Feature scope, architecture |
| **Level 3** | 2 weeks | Strategic, hard to reverse | New system, major pivot |

---

## Key Contacts & Systems

### Mortgage/Finance
- **Regent Bank:** Samuel (new LOC)
- **Title Company:** Brandy (refinance paperwork)
- **Servicers:** ~10 different (Texas Trust CU + various Novus transfers)

### Software
- **Supabase Project:** gcuunlxfgtnppnqkikaz
- **Development:** Claude Code (Opus 4)
- **Hosting:** Netlify
- **Repo:** GitHub (aj-playbooks for standards)

### Communication
- **Team:** iMessage, Apple Notes, Apple Reminders
- **AI:** ChatGPT (team daily use), Claude (JR strategic)

---

## Quick Reference: What's True Now

✅ 77 properties in portfolio
✅ 31 free & clear, ~46 with mortgages
✅ Kalen is GONE (fired Nov 2025)
✅ Jessica handles bill paying + tenant service
✅ Christian handles maintenance + vendors + eviction execution
✅ Cash flow constrained until refinance closes
✅ Auctions paused 1-2 months
✅ All new development in Claude Code
✅ Master Property Data is the foundation
✅ Bill Tracking is #1 priority

---

*This document lives in the aj-playbooks GitHub repo.*
*Claude Code should read this at the start of every session.*
