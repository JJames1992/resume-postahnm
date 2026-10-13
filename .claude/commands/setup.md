# /setup - Initialize Job Search Configuration

# Configure candidate profile, constraints, and job sources for structured search
# Following MadsLorentzen/ai-job-search framework with NJ technical role constraints

## Usage

Execute /setup to configure the job search system. This will:

1. **Create a candidate profile** with your details and constraints
2. **Configure job sources** (LinkedIn, company career pages, etc.)
3. **Set up search strategy** tailored to NJ technical roles
4. **Initialize application tracker** and status monitoring
5. **Prepare CV and cover letter templates** (copy from ai-job-search)

## Step-by-Step Process

### Step 1: Create Candidate Profile
Copy the candidate profile from:
`C:/Users/jonat/.aijob-ref/.claude/skills/job-application-assistant/01-candidate-profile.md`

Modify with your actual information:
- Replace `[YOUR_NAME]` with "Jonathan E. James"
- Update location: "Planning to relocate to Forked River, NJ area (currently Albuquerque, NM)"
- Set constraints: no travel, day shift only, ≥$100K, weekdays only, within 30 min of Forked River NJ
- Add your technical skills, education, experience

Save as: `C:/Users/jonat/OneDrive/Documents/Resume/PostAHNM Job Hunt/.claude/skills/job-application-assistant/01-candidate-profile.md`

### Step 2: Configure Job Search Strategy

Create `search-queries.md` in the kanban board workspace:

```markdown
# Search Queries for Job Scraper

Customized for Jonathan James — NJ-based technical roles.

## Search Strategy
- Primary: LinkedIn CLI (country-specific queries)
- Fallback: WebSearch with `site:` filters for company career pages
- Specialized: Direct queries for NJ technical roles

## Query Categories

### 1. PPPL / Fusion Lab Technician (HIGH PRIORITY — local, mission-aligned)
- "PPPL jobs technician"
- "fusion energy technician jobs New Jersey"
- "PPPL Associate Heating Systems Electrical Technician"

### 2. Technical Writer / Documentation (REMOTE + HIGH PAY)
- "technical writer remote $100K"
- "ISO 9000 technical writer"
- "laboratory documentation specialist"

### 3. Calibration / Metrology (LOCAL, HIGH ALIGNMENT)
- "calibration technician New Jersey"
- "field service engineer NO TRAVEL NJ"
- "IPC-620 technician New Jersey"

### 4. General NJ Technical (BROAD)
- "technician jobs New Jersey remote"
- "$100K technician jobs New Jersey"
- "day shift technician jobs NJ no travel"
```

### Step 3: Setup Outlook Sync

Create `outlook-sync.md` with:

```markdown
# /outlook-sync - Sync Application Status from Outlook Email

You are scanning the user's Outlook email for status signals on tracked job applications.

## Setup
1. Ensure Outlook Graph access is configured
2. Check token cache at `~/AppData/Local/hermes/outlook/token_cache.json`
3. Verify `graph.py mail` works

## Search Strategy
- Query inbox + Sent Items for last 21 days
- Keywords: "interview", "offer", "rejection", "application", "assessment"
- Filter by tracked companies (PPPL, Merck, Johnson & Johnson, etc.)
- Extract: sender, subject, date, body snippet

## Classification
- INTERVIEW_INVITE: "interview" + date/time
- OFFER: "offer" or "congratulations"
- REJECTION: "not proceeding" / "no longer"
- APPLICATION_RECEIVED: "application received" / "submitted"

## Workflow
1. Present classified changes for user approval
2. Update `job_search_tracker.csv` and `outcome.md`
3. Mark processed emails as read
```

### Step 4: Initialize Application Tracking

Create `job_search_tracker.csv`:

```csv
date,source,title,company,location,url,status,applied_date,notes
2026-10-13,LinkedIn,"Associate Heating Systems Electrical Technician",Princeton Plasma Physics Lab (PPPL),"Princeton, NJ (Hamilton Township target)",https://pppl-princeton.icims.com/jobs/21454/associate-heating-systems-electrical-technician/job,DRAFT,2026-10-13,Ready for PPPL application
```

### Step 5: Prepare Application Materials

Copy CV and cover letter templates from ai-job-search:

From `~/.aijob-ref/cv/` and `~/.aijob-ref/cover_letters/` to:
`C:/Users/jonat/OneDrive/Documents/Resume/PostAHNM Job Hunt/documents/applications/`

Customize for Jonathan James profile.

## Automation Script

Create a Python script `setup_jobs.py` in the kanban board workspace:

```python
#!/usr/bin/env python3
"""Initialize job search setup"""

import json
import shutil
from pathlib import Path

def setup_job_search():
    # Copy candidate profile
    profile_src = Path("~/.aijob-ref/.claude/skills/job-application-assistant/01-candidate-profile.md").expanduser()
    profile_dst = Path("C:/Users/jonat/OneDrive/Documents/Resume/PostAHNM Job Hunt/.claude/skills/job-application-assistant/01-candidate-profile.md")
    shutil.copy2(profile_src, profile_dst)
    print(f"✅ Copied candidate profile to {profile_dst}")
    
    # Copy CV templates
    cv_src_dir = Path("~/.aijob-ref/cv/").expanduser()
    cv_dst_dir = Path("C:/Users/jonat/OneDrive/Documents/Resume/PostAHNM Job Hunt/documents/cv/")
    if cv_src_dir.exists():
        shutil.copytree(cv_src_dir, cv_dst_dir, dirs_exist_ok=True)
        print(f"✅ Copied CV templates to {cv_dst_dir}")
    
    # Copy cover letter templates
    cl_src_dir = Path("~/.aijob-ref/cover_letters/").expanduser()
    cl_dst_dir = Path("C:/Users/jonat/OneDrive/Documents/Resume/PostAHNM Job Hunt/documents/cover-letters/")
    if cl_src_dir.exists():
        shutil.copytree(cl_src_dir, cl_dst_dir, dirs_exist_ok=True)
        print(f"✅ Copied cover letter templates to {cl_dst_dir}")
    
    # Initialize search-queries.md
    queries_content = """# Search Queries for Job Scraper

Customized for Jonathan James — NJ-based technical roles.

## Search Strategy
- Primary: LinkedIn CLI
- Fallback: WebSearch with `site:` filters
- Specialized: Direct queries for NJ technical roles

## Query Categories

### 1. PPPL / Fusion Lab Technician
- "PPPL jobs technician"
- "fusion energy technician jobs New Jersey"
- "PPPL Associate Heating Systems Electrical Technician"

### 2. Technical Writer / Documentation
- "technical writer remote $100K"
- "ISO 9000 technical writer"

### 3. Calibration / Metrology
- "calibration technician New Jersey"
- "field service engineer NO TRAVEL NJ"

### 4. General NJ Technical
- "technician jobs New Jersey remote"
- "$100K technician jobs New Jersey"
- "day shift technician jobs NJ no travel"
"""
    
    queries_file = Path("C:/Users/jonat/OneDrive/Documents/Resume/PostAHNM Job Hunt/.claude/skills/job-scraper/search-queries.md")
    queries_file.write_text(queries_content)
    print(f"✅ Created search queries at {queries_file}")
    
    # Create initial job search tracker
    tracker_content = """date,source,title,company,location,url,status,applied_date,notes
2026-10-13,LinkedIn,"Associate Heating Systems Electrical Technician",Princeton Plasma Physics Lab (PPPL),"Princeton, NJ (Hamilton Township target)",https://pppl-princeton.icims.com/jobs/21454/associate-heating-systems-electrical-technician/job,DRAFT,2026-10-13,Ready for PPPL application
2026-10-13,LinkedIn,"Registered Apprenticeship Inquiry",Princeton Plasma Physics Lab (PPPL),"Princeton, NJ (Hamilton Township target)",https://www.pppl.gov/work-with-us/apprenticeships,DRAFT,2026-10-13,Ready for PPPL apprenticeship inquiry
"""
    
    tracker_file = Path("C:/Users/jonat/OneDrive/Documents/Resume/PostAHNM Job Hunt/job_search_tracker.csv")
    tracker_file.write_text(tracker_content)
    print(f"✅ Created job search tracker at {tracker_file}")
    
    print("\n🎉 Job search setup complete!")
    print("Next steps:")
    print("1. Customize 01-candidate-profile.md with your specific details")
    print("2. Run 'python job_search_minimal.py' to start discovery")
    print("3. Use /setup to configure search strategy")
    print("4. Monitor application status with /outlook-sync")

if __name__ == "__main__":
    setup_job_search()
```

## Manual Setup Alternative

If automation is preferred, manually perform the file copies and edits described above.

## Next Steps

1. **Review existing files** in kanban board workspace
2. **Customize** 01-candidate-profile.md with your actual profile
3. **Update** search queries to match your target roles
4. **Initialize** tracking with current applications (the 2 PPPL drafts)
5. **Test** the setup with initial discovery

## Notes

- This setup follows the ai-job-search framework but adds NJ-specific constraints
- All existing PostAHNM Job Hunt files are preserved and enhanced
- The system integrates with existing PPPL applications (currently in Drafts)
- Look for 'pppl' directories in `~/.aijob-ref/.claude/skills/` for specific PPPL workflow
- The setup preserves your existing job search tracker while updating it with current status

## Troubleshooting

### Issues with Profile Setup
- Ensure 01-candidate-profile.md is properly formatted
- Check that all required fields are populated
- Verify constraints are correctly specified

### Search Not Working
- Verify search-queries.md exists and is readable
- Check that job discovery scripts have proper permissions
- Ensure Python dependencies are installed

### Application Tracking
- Validate job_search_tracker.csv format
- Check that application status is accurate
- Verify that tracker entries match actual application progress

This setup script will prepare your workspace for automated job searching while maintaining your existing PostAHNM Job Hunt framework.
