---
name: tech-assessment
description: Generate tech assessment reports for mentor/mentee relationships tracking growth, goals, and action items over time. Use when the mentor says "tech-assessment", "/tech-assessment", or "tech assessment" and provides meeting notes, a transcript, or a summary. The skill produces an updated overview.md and a dated assessment.md archival file.
---

# Tech Assessment

Generate progress reports from mentor-mentee meetings for technical assessment and continuous improvement.

## Step 1: Locate Tech Assessments Directory

Find the directory where tech assessment files are stored. This is typically a nested subfolder within the current working directory.

**Search strategy:**
1. Use `Glob` to search for `**/overview.md` files containing "Tech Assessment Overview" in their content
2. If multiple candidates exist, ask the mentor to confirm which directory to use
3. If no candidates exist, ask the mentor for the assessments directory path

**Confirmation prompt:**
> "Found tech assessments at `<path>`. Is this correct, or provide the correct path."

Once located, store this path as the base for all assessment files.

## Step 2: Identify Mentee

Determine the mentee's name from context or the directory structure found in Step 1.

**If unclear, ask explicitly:**
> "Who is this tech assessment for?"

The mentee name determines the subfolder structure within the assessments directory.

## Step 3: Load Previous Context

Before processing new input, check for existing files:

1. **Look for** `<mentee-name>/overview.md`
2. **Find the most recent** `*-assessment.md` file
3. **Load both** to understand:
   - Active goals and their deadlines
   - Outstanding action items
   - Previous learnings and focus areas

If no previous context exists, note this as the first assessment.

## Step 4: Parse Input

Analyze the provided notes/transcript/summary and extract:

### Current Focus
- Projects the mentee is actively working on
- Responsibilities they're handling
- Areas of concentration

### New Learnings
- **Techniques:** New development approaches, patterns, methodologies
- **Tools:** New frameworks, libraries, software, platforms
- Note: Learnings can come from either mentor or mentee

### Goals Progress
- Goal description
- Deadline
- Current status (On Track / At Risk / Behind)
- Progress notes or blockers

### Action Items
- Task description
- Due date
- Owner (mentee/mentor/both)
- Status (New / Carried Over / Completed / Overdue)

### Overdue Items
Compare all goals and action items from previous context against today's date. Identify any that are overdue and flag them for follow-up with the mentor.

## Step 5: Identify Missing Information

After parsing, check what's missing. If any of these cannot be inferred, prompt the mentor:

| Element | Prompt if Missing |
|---------|-------------------|
| Current focus | "What projects is {{mentee}} currently working on?" |
| New learnings | "Any new techniques or tools discussed?" |
| Goals | "What goals should we track?" |
| Goal deadlines | "What is the deadline for {{goal}}?" |
| Action items | "What action items were identified?" |
| Action item deadlines | "What is the due date for {{action item}}?" |
| Goal status | "How is {{mentee}} progressing toward each goal?" |
| Overdue items | "The following items are overdue: {{list}}. What's the status? Should deadlines be adjusted?" |

**Deadline requirement:** Every goal and action item must have a deadline. Always ask for deadlines if not provided.

Be specific in prompts - reference the input provided to show what was found and what's missing.

## Step 6: Generate Outputs

### Output 1: Update `overview.md`

Update the living document using the template at [assets/overview.md](assets/overview.md).

### Output 2: Create `YYYY-MM-DD-assessment.md`

Create a dated archival file using the template at [assets/assessment.md](assets/assessment.md).

Key elements:
- Link to previous assessment
- Discussion summary
- Current focus (snapshot)
- New learnings (snapshot)
- Goals progress table showing previous vs current status
- Action items (carried over + new)
- Notes for next assessment

---

## File Structure

When creating new assessment files, organize within the assessments directory identified in Step 1:

```
<assessments-directory>/
└── <mentee-name>/
    ├── overview.md              # Living document, update after each assessment
    ├── 2025-02-05-assessment.md # Archived assessments
    ├── 2025-02-12-assessment.md
    └── ...
```

Always use lowercase mentee-name with hyphens for spaces (e.g., `john-doe`).