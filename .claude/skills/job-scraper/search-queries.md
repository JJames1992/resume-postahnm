# Search Queries for Job Scraper

Customized for Jonathan James — NJ-based technical roles.

## Installed portal CLIs (primary for /scrape)
- **linkedin.com/jobs** — LinkedIn job listings (filter: Princeton, NJ / Forked River, NJ; remote)
- **indeed.com** — Indeed job search via headless browser
- **pppl.gov/careers** — Direct company career page

## WebSearch fallback site: queries
Primary targets (company career pages via Google):
- `site:pppl.gov careers technician` — PPPL always first
- `site:princeton.gov careers` — Princeton Borough/Township jobs
- `site:merck.com careers technician` — Merck (Rahway, 20 min from Forked River)
- `site:jnj.com careers technician` — Johnson & Johnson (New Brunswick)
- `site:gsk.com careers technician` — GSK (Parsippany/Whippany)

## Search query categories (WebSearch fallback)

### 1. PPPL / Fusion Lab Technician (HIGH PRIORITY — local, mission-aligned)
- "PPPL jobs technician" OR "Princeton Plasma Physics Lab careers technician"
- "fusion energy technician jobs New Jersey"
- "PPPL Associate Heating Systems Electrical Technician"
- "NSTX-U technician positions"
- "DOE national lab technician jobs NJ"

### 2. Technical Writer / Documentation (REMOTE + HIGH PAY)
- "technical writer remote $100K" OR "senior technical writer remote NJ"
- "documentation specialist day shift remote"
- "ISO 9000 technical writer"
- "laboratory documentation specialist"

### 3. Calibration / Metrology (LOCAL, HIGH ALIGNMENT)
- "calibration technician New Jersey" OR "metrology technician NJ"
- "calibration technician day shift Princeton"
- "field service engineer NO TRAVEL NJ"
- "calibration technician remote hybrid"
- "IPC-620 technician New Jersey"

### 4. Field Service / Lab Support (NO TRAVEL ONLY)
- "lab technician Princeton NJ" OR "laboratory technician New Brunswick"
- "HVAC technician national lab"
- "electro-mechanical technician PPPL"
- "instrumentation technician Princeton"

### 5. General NJ Technical (BROAD)
- "technician jobs New Jersey remote"
- "$100K technician jobs New Jersey"
- "day shift technician jobs NJ no travel"

## Query language
All queries in English. Filter for: day shift only, no overnight travel, ≥$100K (or remote with high pay), within 30 min of Forked River or fully remote.

## Location targets
- Princeton, NJ (primary — PPPL)
- Forked River, NJ (primary — Amelia)
- Hamilton Township, NJ (within 30 min of Forked River)
- New Brunswick, NJ (within 45 min)
- Remote (US-based)

## Exclusion keywords (hard filter — never show these)
- "travel required"
- "overnight travel"
- "25% travel"
- "50% travel"
- "80% travel"
- "field service" (unless "no travel" accompanies)
- "relocation provided" (implies travel/hybrid)
