# DL Course Review Portal

Tuskegee University · Office of Teaching and Innovation

A reusable review portal. The Google Sheet is the database. The web page never
changes between terms: courses, reviewers, PINs, the rubric, and the term are
all read from the Sheet.

| File | Purpose | Where it goes |
|---|---|---|
| `index.html` | The portal | GitHub Pages |
| `apps-script/Code.gs` | Turns the Sheet into the database | The Sheet's Apps Script editor |
| `DL_Course_Review_Import_Template.xlsx` | Optional blank course-list layout | Keep for reference |

## One-time setup (about 15 minutes)

### 1. Create the Sheet

1. Go to sheets.google.com and create a blank spreadsheet.
2. Name it `DL Course Review Portal - Database`.

### 2. Install the script

1. In the Sheet: **Extensions > Apps Script**.
2. Select everything in the editor and delete it.
3. Open `apps-script/Code.gs`, copy all of it, paste it into the editor, and press **Save**.
4. Confirm the function menu at the top (next to the Debug button) shows **setup**. If it shows another name, click it and choose **setup**. Then press **Run**.
5. Approve the permission prompt (Advanced > Go to project > Allow). The first run may stop after approval; if so, press **Run** again.
6. Return to the Sheet. Six tabs now exist: Settings, Reviewers, Courses, Rubric, Reviews, Remediation. A message also appears in the lower right of the Sheet.

**If no tabs appear:**

- The function menu showed `doPost` or `onOpen` instead of `setup`. Select **setup** and run again.
- The script was created at script.google.com instead of from the Sheet. The execution log then says the script is not attached to a Google Sheet. Delete that project, open the Sheet, and use **Extensions > Apps Script**.
- The Sheet tab was already open. Reload the Sheet's browser tab.

### 3. Enter PINs

1. Open the **Reviewers** tab.
2. Type a 4-digit PIN in the PIN column for each person.
3. Confirm the Programs column (for example `CAENS`, `SOWK`, `GEN`). Separate several programs with commas.
4. Confirm the Instructor Name column. It is the name as it appears in course lists, and it prevents a reviewer from being assigned a course they teach.

Use new PINs. The Summer and Fall 2026 PINs are visible in the source of those earlier portals.

### 4. Deploy the script

1. In Apps Script: **Deploy > New deployment**.
2. Gear icon > **Web app**.
3. Execute as: **Me**. Who has access: **Anyone**.
4. Press **Deploy** and copy the **Web app URL**.

### 5. Connect the portal

1. Open `index.html` (on GitHub, use the pencil icon).
2. Search for `PASTE_YOUR_APPS_SCRIPT_WEB_APP_URL_HERE`.
3. Replace that text with the Web app URL. Keep the quotation marks.
4. Commit the change.

### 6. Publish

1. Create a new GitHub repository, for example `dl-review-portal`.
2. Upload `index.html`.
3. **Settings > Pages > Branch: main > Save**.
4. Open the Pages address and sign in with your name and PIN.

Leave the Fall 2026 portal and its repository as they are until that cycle closes.

## Each term

1. Sign in as supervisor. **Settings > Current term** (for example `Summer 2027`) > **Save**.
2. **Import courses** and choose the term's Excel or CSV file.
3. Confirm the column matches and the reviewer assignments, then press **Import**.

A later file for the same term adds only the new courses. Existing courses keep their reviewer and progress.

## How a course moves

| Stage | Meaning | What moves it forward |
|---|---|---|
| Assigned | No ratings yet | Reviewer begins rating |
| In Review | Some items rated | Reviewer submits the review |
| Action Required | Submitted with Not Met items | Reviewer records that feedback was sent |
| Revisions In Progress | Instructor is making changes | Reviewer marks each item completed |
| Certified | All items Met, or all follow-up items completed | Final |

The supervisor can certify or hold any submitted course with an outcome override, and can reopen any review.

## Routine changes (all in the Sheet, no code)

| To do this | Edit this |
|---|---|
| Add, remove, or deactivate a reviewer | Reviewers tab (set Active to `No` to remove access at once) |
| Change a PIN | Reviewers tab, PIN column |
| Change which programs a reviewer covers | Reviewers tab, Programs column |
| Reword, add, or retire a rubric item | Rubric tab (set Active to `No` to retire; keep the Item ID of existing items unchanged) |
| Change the revision window | Settings tab, Revision Days |
| Rename the office | Settings tab, Office Name |

Changes take effect at the next sign-in or when **Refresh** is pressed.

## If the script is edited later

After any change to `Code.gs`: **Deploy > Manage deployments > Edit > Version: New version > Deploy**. The URL stays the same.
