# Plan: Update `1481 Lab Guide[UPDATED].docx` to Match `docs/index.html`

## Top-Level Overview

Sync `1481 Lab Guide[UPDATED].docx` with all changes made to `docs/index.html` in the previous session.
The HTML is the source of truth. The docx has been read and mapped. Eight distinct edits are needed.

**File access:** `*.docx` is currently commented out of `.gitignore` (user did this manually). No Sub-Task 0 needed.

**Versioning:** All edits are made to a NEW copy of the file — `1481 Lab Guide[UPDATED]-v2.docx`. The original is never touched.

**Images:** Relevant screenshots from `docs/images/pa/` will be embedded (not path-referenced) into the new docx. Embedded images are fully portable — they travel with the file when uploaded anywhere. They may need manual resizing in Word after insertion.

---

## Docx Structure As-Found (reference)

| Docx section | Heading text | Para path |
|---|---|---|
| Title | 1481: Build AI-Powered Staff Schedules… | `/body/p[@paraId=34651B72]` |
| 1 | Introduction | `/body/p[@paraId=6F7DE373]` |
| 1.1 | About this hands-on lab | `/body/p[@paraId=63DE9F88]` |
| 2 | Lab Set Up | `/body/p[@paraId=45227955]` |
| 2.1 | Access Lab Files | `/body/p[@paraId=24B90012]` |
| 2.2 | Setting up Bob | `/body/p[@paraId=10E3AAB7]` |
| 3 | Lab Instructions! | `/body/p[@paraId=79C78E84]` |
| 3.1 | Understanding your data | `/body/p[@paraId=3F76197A]` |
| 3.2 | Building out your Optimization problem… | `/body/p[@paraId=77DEAF0A]` |
| 3.3 | Deploying and testing out your solution | `/body/p[@paraId=527113F1]` |
| 3.4 | Running your Optimization model in Planning Analytics | `/body/p[@paraId=5B0D7DA8]` |
| 3.4.1 | Setup a deployment execution script… | `/body/p[@paraId=3A38F5C5]` |
| 3.4.1.1 | "3.4.1.1 Create a new workbench" | `/body/p[@paraId=02225B70]` |
| 3.4.1.2 | Create new Process in your Workbench | `/body/p[@paraId=308E4C7D]` |
| 3.4.1.3 | Create Deployment Execution Script… | `/body/p[@paraId=5F5E9184]` |
| 3.4.1.4 | Test Deployment Script | `/body/p[@paraId=1CADD035]` |
| 3.4.2 | Create a Book to run the deployment | `/body/p[@paraId=0B8D0664]` |
| 3.4.3 | Run the model from the Planning Analytics Book. | `/body/p[@paraId=26CE3931]` |

**Key findings from the docx read:**
- There is **no Prompt A** anywhere in the docx — it's entirely absent. Section 3.1 ("Understanding your data") goes straight to the notebook steps with no mention of Prompt A or `data_loader.py`. Same for 3.2. No Sub-Task needed to "move" it — it needs to be **added**.
- There is **no "Planning Analytics Step 1: Review the staffing challenge"** — section 3.1 opens directly with notebook steps. The PA orientation step exists only in the HTML, not the docx.
- There is **no DEPLOYMENT_ID callout** after Prompt 4.3 — the deploy section (3.3) is 4 plain steps with no callout.
- Section **3.4.2** (Create a Book) currently has **13 steps** (steps 1–13 + an optional step 14), exactly the old flow.
- Section **3.4.3** (Run the model) currently has **3 steps** — the old flow.
- There is **no Wrap-Up section**.
- The heading `3.4.1.1` has a text bug: it reads `"3.4.1.1 3.4.1.1 Create a new workbench"` (doubled).
- The TOC is a Word content-control (`[sdt]`) — it auto-updates when headings change; no manual edit needed.

---

## Sub-Tasks

---

### Sub-Task 0 — Create v2 copy of the document

**Intent:** Copy `1481 Lab Guide[UPDATED].docx` to `1481 Lab Guide[UPDATED]-v2.docx` so all edits happen on a new file and the original is preserved.

**Expected Outcomes:**
- `1481 Lab Guide[UPDATED]-v2.docx` exists in the workspace root
- All subsequent sub-tasks operate on the v2 file

**Todo List:**
1. Use PowerShell `Copy-Item` to copy `"1481 Lab Guide[UPDATED].docx"` → `"1481 Lab Guide[UPDATED]-v2.docx"`
2. Verify v2 file exists and is readable via `office_read mode:outline`

**Status:** [ ] pending

---

### Sub-Task 1 — Add "Planning Analytics Step 1" to Data Exploration (section 3.1)

**Intent:** Section 3.1 in the docx ("Understanding your data") currently starts directly with notebook steps. In the HTML, this section starts with a PA orientation step (review the staffing challenge dashboard) *before* the notebook. Add that PA orientation step as a numbered list before the existing notebook steps.

**Expected Outcomes:**
- Section 3.1 gains a clearly labeled "Planning Analytics Step 1: Review the staffing challenge" sub-heading
- 5 steps added: open PA, click Shared, navigate HR_Optimization/shared, open the dashboard, review Today's Challenge tab + read-only callout note
- Existing notebook steps follow after it (unchanged)

**Todo List:**
1. Locate the first paragraph of section 3.1 content (`/body/p[@paraId=2B1269EC]` — "1. In Bob…")
2. Insert before it: a sub-heading "Planning Analytics Step 1: Review the staffing challenge"
3. Insert 5 numbered steps (from HTML `#review-dashboard`) + a "read-only" note
4. After step 1, embed `docs/images/pa/pa-nav-shared.png`
5. After step 3, embed `docs/images/pa/pa-shared-folder.png`
6. After step 5, embed `docs/images/pa/pa-dashboard-open.png`
7. The original notebook steps remain as-is after the new content

**Relevant Context:**
- HTML section: `#review-dashboard` — 5 `<li>` steps + `.callout warn` read-only note
- Existing docx section 3.1 first content para: `paraId=2B1269EC`
- Images: `pa-nav-shared.png`, `pa-shared-folder.png`, `pa-dashboard-open.png`

**Status:** [ ] pending

---

### Sub-Task 2 — Add Prompt A to section 3.2 (Optimizer Build)

**Intent:** Prompt A (`data_loader.py`) exists in the HTML but is completely absent from the docx. It belongs in section 3.2 as the first prompt (before Prompt 3.1), with a row added to the prompt index table.

**Expected Outcomes:**
- A new sub-heading "Prompt A — Generate `data_loader.py`" added in section 3.2, before Prompt 3.1
- The full Prompt A text block added (the long PA data structure description)
- A "Step 2 prompt index" note or table updated to include row A: location "Step 2, after MDX helpers", output "`data_loader.py` — reads PA, validates, caches to JSON"

**Todo List:**
1. Locate the start of section 3.2 content in the docx (first para after `paraId=77DEAF0A`)
2. After the existing step 3 (run prompts instructions), insert sub-heading "Prompt A — Generate `data_loader.py`"
3. Insert full Prompt A text (from HTML `#prompt-A` pre block)
4. Add a note that this prompt produces `data_loader.py`

**Relevant Context:**
- HTML: `#prompt-A` card — full prompt text is in `docs/index.html` lines ~697–769
- Docx section 3.2 ends at `paraId=71739E8B`

**Status:** [ ] pending

---

### Sub-Task 3 — Add DEPLOYMENT_ID callout to section 3.3 + update section 3.4.1.3

**Intent:** After the deploy step instructions in section 3.3, add a callout telling students to note their `DEPLOYMENT_ID` from `step_4_bob.ipynb` Cell 4 output — they'll need it in section 3.4.1.3 (formerly 3.4.1.3, to be renumbered to 5.1.3 later). Also update the `sDeploymentID` line in section 3.4.1.3 to reference Prompt 4.3 as the source.

**Expected Outcomes:**
- After the last step of section 3.3, a clearly formatted "Important" callout/note: "Before moving to section 3.4, note your `DEPLOYMENT_ID` from the output of `step_4_bob.ipynb` Cell 4 (Prompt 4.3). You will need it in section 3.4.1.3."
- In section 3.4.1.3, step 3, the `sDeploymentID = '';` line updated to add: "(get this value from `step_4_bob.ipynb` Cell 4 output — Prompt 4.3. Complete section 3.3 first if you haven't already.)"

**Todo List:**
1. Locate the last paragraph of section 3.3 content (`paraId=2300DAC5` — step 4)
2. Insert the DEPLOYMENT_ID callout note after step 4
3. After the callout text, embed `docs/images/pa/deployment-id-notebook.png`
4. Locate the `sDeploymentID` line in section 3.4.1.3 (`paraId=45D8276C`)
5. Update that paragraph to add the reference note

**Relevant Context:**
- HTML: `callout warn` after Prompt 4.3 card; section `#pa-create-script` step 3b
- `session-summary.md` § "DEPLOYMENT_ID threading"
- Image: `deployment-id-notebook.png`

**Status:** [ ] pending

---

### Sub-Task 4 — Renumber PA section headings: 3.4.x → 5.x

**Intent:** Rename all heading texts from `3.4.x` scheme to `5.x` to match the dashboard. Also fix the doubled heading bug in 3.4.1.1.

**Expected Outcomes:**
- Heading text changes (find_replace, most-specific first):
  - `"3.4.1.1 3.4.1.1 Create a new workbench"` → `"5.1.1 Create a new workbench"` (fixes double too)
  - `"3.4.1.2"` refs → `"5.1.2"` (heading + any inline)
  - `"3.4.1.3"` refs → `"5.1.3"`
  - `"3.4.1.4"` refs → `"5.1.4"`
  - `"3.4.1"` refs → `"5.1"`
  - `"3.4.2"` refs → `"5.2"`
  - `"3.4.3"` refs → `"5.3"`
  - `"3.4"` refs → `"5"` (top-level section heading)
- TOC will auto-update on next Word open (no manual action needed)

**Todo List:**
1. `find_replace` `"3.4.1.1 3.4.1.1 Create a new workbench"` → `"5.1.1 Create a new workbench"`
2. `find_replace` `"3.4.1.2"` → `"5.1.2"`
3. `find_replace` `"3.4.1.3"` → `"5.1.3"`
4. `find_replace` `"3.4.1.4"` → `"5.1.4"`
5. `find_replace` `"3.4.1"` → `"5.1"`
6. `find_replace` `"3.4.2"` → `"5.2"`
7. `find_replace` `"3.4.3"` → `"5.3"`
8. `find_replace` `"3.4 "` → `"5 "` (space-padded to avoid matching `3.4.x` already done)

**Relevant Context:**
- `session-summary.md` § "PA section numbering fix"
- Heading para IDs from outline above

**Status:** [ ] pending

---

### Sub-Task 5 — Rewrite section 3.4.2 (Create Book): 13-step → 6-step flow

**Intent:** Replace the existing 13-step manual widget-by-widget procedure with the streamlined 6-step `Ctrl+Q` / `dashboard.json` paste workflow.

**Old steps to remove (steps 3–13 + step 14):**
- Step 3: Click Widgets → Action Button
- Step 4: Change button title to "Run Optimization Model"
- Step 5: Properties → Configure → Run Process → set Database, Process, Refresh
- Step 6: Click Widgets → Explorations tile
- Step 7: Database logo → expand HR_Optimization → drag Budget Control
- Step 8: Three dots → Open set editor (columns)
- Step 9: Remove Total Budget Cap through Night Band Max FTE, Apply
- Step 10: Three dots → rows → Open set editor
- Step 11: Remove all Members except your name
- Step 12: Swap rows and columns
- Step 13: Save
- Step 14: Optional — repeat for other cubes

**New 6 steps:**
1. Click the hamburger menu, then **New**, then **Book**. *(same wording as docx — no change)*
2. Click the **Save** icon, then click the **Shared** tab, then select the `HR_Optimization` folder. In the Name field type `HR_Opt_Book_[FirstNameLastName]`, then click **Save**. *(docx version is missing "then click Save" — rewrite)*
3. Press `Ctrl+Q` then `/` (Mac: `Cmd+Q` then `/`) to open the spec editor
4. Open `dashboard.json` from your lab files, copy its entire contents, paste into the spec editor, then click the blue **Update** button. *(Note: replace all existing content — do not append.)*
5. Navigate to the **Run Optimization** tab — confirm the blue Run Optimization button and results grid appear
6. Click the **Run Optimization** button once to select it, then click **Properties** (upper-right) → **Configure** tab. Verify: Run Process is toggled ON, Database = `HR_Optimization`, Process = `RunStaffOptimization_[YourFirstNameYourLastName]`, "Refresh after execution" is checked. If anything is missing, set it now and save.

**Expected Outcomes:**
- Step 1 wording confirmed identical — kept as-is
- Step 2 reworded to match HTML (adds "then click Save")
- Old steps 3–14 replaced with new steps 3–6

**Todo List:**
1. Locate section 3.4.2 content paras (from `paraId=0373230C` through `paraId=209667F3`)
2. Rewrite step 2 paragraph (`paraId=163693B7` / `paraId=0C33ED67`) to add "then click Save"
3. Remove old steps 3–14 (paragraphs from `paraId=21DBDDFB` through `paraId=209667F3`)
4. Insert new step 3 text + embed `docs/images/pa/pa-board-spec-window.png`
5. Insert new step 4 text + embed `docs/images/pa/pa-book-save-dialog.png` (reuse — shows save dialog)
6. Insert new step 5 text + embed `docs/images/pa/pa-tab-run-optimization.png`
7. Insert new step 6 text + embed `docs/images/pa/pa-book-configure-process.png` + `pa-book-configure-panel.png`

**Relevant Context:**
- `session-summary.md` § "Section 5.2 rewrite"
- HTML section `#pa-book`
- Images: `pa-board-spec-window.png`, `pa-book-save-dialog.png`, `pa-tab-run-optimization.png`, `pa-book-configure-process.png`, `pa-book-configure-panel.png`

**Status:** [ ] pending

---

### Sub-Task 6 — Rewrite section 3.4.3 (Run + Review): 3-step → 6-step tab review

**Intent:** Expand the 3-step "toggle, click, see results" section to 6 steps with a tab-by-tab description of what students should see in the results.

**Old 3 steps:**
1. Toggle Edit to OFF
2. Click Run Optimization Model
3. View the results in the Exploration view after the job completes

**New 6 steps:**
1. Toggle Edit to OFF
2. Click **Run Optimization Model** and wait 60–90 seconds for the results grid to appear
3. **Results Summary tab** — review 3 KPI tiles: Budget Used, Hire Slots Activated, Merit Pool Deployed
4. **Headcount Plan tab** — review which hire slots were activated (1.00) vs. skipped (0.00)
5. **Schedule tab** — review 12 clinicians' band assignments; 11 of 12 should be on their preferred shift
6. **Merit & Retention tab** — review merit awards; note that raises are not purely risk-ranked — the optimizer balances merit ROI with skill and seniority

**Expected Outcomes:**
- Old steps 2–3 replaced with steps 2–6 above (step 1 "Toggle Edit OFF" is the same)

**Todo List:**
1. Locate section 3.4.3 content paras (`paraId=5B5C649D` through `paraId=413F9336`)
2. Rewrite step 1 to match HTML wording (add "using the toggle in the top-left of the Book toolbar") + embed `docs/images/pa/pa-book-edit-toggle-off.png`
3. Remove old steps 2–3 (`paraId=47633A85` and `paraId=413F9336`)
4. Insert new step 2 text + embed `docs/images/pa/pa-tab-run-optimization.png`
5. Insert new step 3 text + embed `docs/images/pa/pa-tab-results-summary.png`
6. Insert new step 4 text + embed `docs/images/pa/pa-tab-headcount-plan.png`
7. Insert new step 5 text + embed `docs/images/pa/pa-tab-schedule.png`
8. Insert new step 6 text + embed `docs/images/pa/pa-tab-merit-retention.png`

**Relevant Context:**
- `session-summary.md` § "Section 5.3 rewrite"
- HTML section `#pa-run`
- Images: `pa-book-edit-toggle-off.png`, `pa-tab-run-optimization.png`, `pa-tab-results-summary.png`, `pa-tab-headcount-plan.png`, `pa-tab-schedule.png`, `pa-tab-merit-retention.png`

**Status:** [ ] pending

---

### Sub-Task 7 — Add Wrap-Up section at end of document

**Intent:** Add a new final section after 3.4.3 (before the legal notices), equivalent to the `#wrapup` section in the HTML dashboard.

**Expected Outcomes:**
- New Heading 2: "Wrap-Up"
- Architecture overview paragraph: 3-pillar flow (Planning Analytics → CPLEX optimizer → watsonx.ai, with write-back to PA)
- Bulleted list of 5 artifacts: `data_loader.py`, `step_123_bob.ipynb`, `score_clinical_optimizer.py`, watsonx.ai batch endpoint, PA Book + TI script
- "The pattern you can take forward" paragraph
- "What IBM Bob made possible" paragraph

**Todo List:**
1. Locate the last content paragraph before the legal notices (`paraId=3B94081D` and nearby blank paras)
2. Add Heading 2 paragraph: "Wrap-Up"
3. Add architecture overview paragraph (3-pillar description)
4. Add bulleted list of 5 artifacts
5. Add "The pattern you can take forward" paragraph (from HTML `#wrapup`)
6. Add "What IBM Bob made possible" paragraph (from HTML `#wrapup`)

**Relevant Context:**
- `session-summary.md` § "Wrap-Up section (new, #wrapup)"
- HTML section `#wrapup` — read full paragraph text from `docs/index.html` before inserting

**Status:** [ ] pending

---

### Sub-Task 8 — Minor fixes: section 3.3 notebook name + section heading cleanup

**Intent:** Section 3.3 in the docx refers to `"step4_bob.ipynb"` but the actual file is `step_4_bob.ipynb` (underscores). Fix the filename. Also the section 3 top heading is `"Lab Instructions!"` — the exclamation mark is informal; optionally normalize but only if client agrees.

**Expected Outcomes:**
- `"step4_bob.ipynb"` → `"step_4_bob.ipynb"` in section 3.3 step 1
- (Optional) `"Lab Instructions!"` → `"Lab Instructions"` — only if approved

**Todo List:**
1. `find_replace` `"step4_bob.ipynb"` → `"step_4_bob.ipynb"`
2. Confirm with user whether to normalize the `!` in "Lab Instructions!"

**Relevant Context:**
- Docx para `paraId=3443B827` — step 1 of section 3.3

**Status:** [ ] pending

---

## Pending HTML → Docx Sync (Round 2)

Changes made to `docs/index.html` after the v2 docx was created. Each item below must be applied to `1481 Lab Guide v2.docx` in the next docx edit session.

---

### H1 — Lab Setup step 2: "Open the zip file" → extract instruction

**HTML change:** Step 2 under "Access Lab Files" changed from:
> Open the zip file.

to:
> Extract the zip file to a folder in the Downloads folder.

**Docx location:** Section 2.1 (Access Lab Files), step 2 — the paragraph currently reading "2. Open the zip file."

**Action:** `find_replace` `"Open the zip file."` → `"Extract the zip file to a folder in the Downloads folder."`

**Status:** [ ] pending

---

### H2 — Lab Setup step 4: clarify SETUP.md reference and terminal usage

**HTML change:** Step 4 under "Setting up Bob" changed from:
> Follow the instructions in the file to create and activate your Python virtual environment that you will be using throughout this lab.

to:
> Follow the instructions in the `SETUP.md` file to create and activate your Python virtual environment that you will be using throughout this lab. Use the terminal that you opened to execute any commands.

**Docx location:** Section 2.2 (Setting up Bob), step 4.

**Action:** `find_replace` `"Follow the instructions in the file to create and activate your Python virtual environment that you will be using throughout this lab."` → `"Follow the instructions in the SETUP.md file to create and activate your Python virtual environment that you will be using throughout this lab. Use the terminal that you opened to execute any commands."`

**Status:** [ ] pending

---

