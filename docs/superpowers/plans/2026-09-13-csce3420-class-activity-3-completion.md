# CSCE 3420 Class Activity 3 Completion Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox syntax for tracking.

**Goal:** Complete the supplied CSCE 3420 worksheet and its required semantic HTML project with 13 readable terminal evidence screenshots.

**Architecture:** Keep the source project portable and self-contained under Williams_Clyde_CSCE3420_ClassActivity3/. Use static HTML with relative links and one local SVG asset. Use a separate evidence workflow to display one raw command and real output per fullscreen terminal capture, then insert those PNGs into the worksheet.

**Tech Stack:** HTML5, SVG, Git, GitHub SSH, Ubuntu Terminal, ImageMagick import, LibreOffice, Python managed by uv with python-docx, lxml, and beautifulsoup4.

**Spec:** docs/superpowers/specs/2026-09-13-csce3420-class-activity-3-design.md

## Global Constraints

- Student: Clyde Williams, ID 11826899, Section 001, Date 9/6/2026.
- Commit identity: local repo only, Clyde Williams <ClydeWilliams@my.unt.edu>.
- Remote: git@github.com:clydew372/csce3420-class-activity-3.git.
- Evidence images: exactly 1920x1200, fullscreen root capture, maximized Ubuntu Terminal, stock prompt colors, raw commands only.
- Worksheet output: preserve original formatting; remove rubric, TA grading guidelines, and activity completion checklist.
- DOCX reads and writes: run through a uv managed environment.

### Task 1: Prepare the UV Environment and Project Skeleton

**Files:**
- Create: Williams_Clyde_CSCE3420_ClassActivity3/index.html
- Create: Williams_Clyde_CSCE3420_ClassActivity3/pages/about.html
- Create: Williams_Clyde_CSCE3420_ClassActivity3/images/semantic-map.svg
- Create: Williams_Clyde_CSCE3420_ClassActivity3/media/.gitkeep

**Interfaces:**
- Produces the project root, relative path layout, and local image path used by later pages and screenshots.

- [ ] Step 1: Create the UV environment

~~~bash
uv venv .venv
uv pip install --python .venv/bin/python python-docx lxml beautifulsoup4
~~~

Expected: .venv/bin/python exists and the packages install successfully.

- [ ] Step 2: Add the initial HTML5 foundation

Create index.html with doctype, lang="en", UTF-8, viewport, title, meta description, header, nav, main, one h1, and footer. Keep navigation links relative and include id="coursework" on the coursework section.

- [ ] Step 3: Add the local image and about page

Create images/semantic-map.svg with visible landmark labels and pages/about.html with a valid HTML5 document and a return link whose exact href is ../index.html.

- [ ] Step 4: Run a skeleton check

~~~bash
uv run --with beautifulsoup4 python -c "from bs4 import BeautifulSoup; from pathlib import Path; p=Path('Williams_Clyde_CSCE3420_ClassActivity3/index.html'); s=BeautifulSoup(p.read_text(), 'html.parser'); assert s.html.get('lang') == 'en'; assert len(s.find_all('h1')) == 1; assert s.find('section', id='coursework'); print('foundation ok')"
~~~

Expected: foundation ok.

- [ ] Step 5: Commit the foundation

~~~bash
git add Williams_Clyde_CSCE3420_ClassActivity3
git commit -m "feat: add HTML5 foundation and semantic landmarks"
~~~

### Task 2: Complete Guided Page Content

**Files:**
- Modify: Williams_Clyde_CSCE3420_ClassActivity3/index.html

**Interfaces:**
- Consumes the Task 1 foundation and image path.
- Produces navigation, semantic sections, article, aside, heading outline, meaningful image, lists, data table, and accessible form required by screenshots 2 through 7.

- [ ] Step 1: Add semantic content and heading hierarchy

Use exactly one h1, at least three h2 headings, and an h3 nested under an h2. Include multiple paragraphs with meaningful strong and em usage. Put main content in distinct sections, place a self-contained explanation in an article, and place secondary guidance in an aside.

- [ ] Step 2: Add all four navigation behaviors

~~~html
<a href="index.html">Home</a>
<a href="pages/about.html">About</a>
<a href="#coursework">Coursework</a>
<a href="https://developer.mozilla.org/en-US/docs/Web/HTML">MDN HTML Reference</a>
~~~

- [ ] Step 3: Add image, lists, table, and form

Use the SVG with a descriptive alt value and width. Add an unordered list of topics, an ordered workflow list, a captioned table with thead, tbody, three columns, four data rows, and scope="col" headers. Add labeled text, email, select, textarea, checkbox, and submit controls.

- [ ] Step 4: Run the guided-page structural check

~~~bash
uv run --with beautifulsoup4 python - <<'PY'
from bs4 import BeautifulSoup
from pathlib import Path
p=Path('Williams_Clyde_CSCE3420_ClassActivity3/index.html')
s=BeautifulSoup(p.read_text(), 'html.parser')
assert len(s.find_all('h1')) == 1
assert len(s.find_all('h2')) >= 3 and s.find('h3') is not None
assert s.find('img').get('alt') and s.find('img').get('width')
assert len(s.find_all('ul')) >= 1 and len(s.find_all('ol')) >= 1
table=s.find('table'); assert table.find('caption') and len(table.select('thead th')) >= 3 and len(table.select('tbody tr')) >= 4
form=s.find('form'); assert form and len(form.find_all(['input','select','textarea','button'])) >= 4
for label in form.find_all('label'): assert form.find(id=label.get('for'))
print('guided page ok')
PY
~~~

Expected: guided page ok.

- [ ] Step 5: Commit guided content

~~~bash
git add Williams_Clyde_CSCE3420_ClassActivity3/index.html
git commit -m "feat: add navigation media lists and table"
~~~

### Task 3: Add Debug and Independent Profile Pages

**Files:**
- Create: Williams_Clyde_CSCE3420_ClassActivity3/debug.html
- Create: Williams_Clyde_CSCE3420_ClassActivity3/profile.html

**Interfaces:**
- Produces corrected debug markup and an independent profile document for screenshots 9 and 13.

- [ ] Step 1: Correct supplied debug issues

Create valid debug.html with the missing h1 close, corrected heading close, closing main, body, and html tags, useful image alt text and an image path that exists, plus a working external href.

- [ ] Step 2: Build a structurally distinct profile page

Create a profile page whose main flow uses an article, a figure, separate sections, an aside, a list, a table, an internal fragment link, an external link, and a labeled form. Use content and section names distinct from index.html, one h1, and at least three paragraphs.

- [ ] Step 3: Run profile and debug checks

~~~bash
uv run --with beautifulsoup4 python - <<'PY'
from bs4 import BeautifulSoup
from pathlib import Path
for name in ('debug.html','profile.html'):
    s=BeautifulSoup(Path('Williams_Clyde_CSCE3420_ClassActivity3', name).read_text(), 'html.parser')
    assert s.html.get('lang') == 'en' and s.title and s.find('meta', attrs={'name':'description'})
    assert len(s.find_all('h1')) == 1
assert BeautifulSoup(Path('Williams_Clyde_CSCE3420_ClassActivity3/debug.html').read_text(), 'html.parser').find('img').get('alt')
print('debug and profile ok')
PY
~~~

Expected: debug and profile ok.

- [ ] Step 4: Commit remaining source pages

~~~bash
git add Williams_Clyde_CSCE3420_ClassActivity3/debug.html Williams_Clyde_CSCE3420_ClassActivity3/profile.html
git commit -m "feat: add debugging exercise and independent profile"
~~~

### Task 4: Validate, Commit, and Push

**Files:**
- Modify: Git history and remote repository only

**Interfaces:**
- Consumes all source files.
- Produces validator output, three meaningful development commits, and a synchronized remote tree.

- [ ] Step 1: Run local HTML checks

Run the structural checks from Tasks 2 and 3, then run `uv run --with html5validator html5validator Williams_Clyde_CSCE3420_ClassActivity3 --also-check-css=false`. Record the final result for the worksheet response.

- [ ] Step 2: Confirm local commit identity and history

~~~bash
git config --local --get user.email
git --no-pager log --oneline --decorate -5
~~~

Expected: ClydeWilliams@my.unt.edu and three meaningful feature commits.

- [ ] Step 3: Add and push the supplied remote

~~~bash
git remote add origin git@github.com:clydew372/csce3420-class-activity-3.git
git push -u origin activity3-completion:main
~~~

Expected: remote main contains the required source files.

### Task 5: Produce Terminal Evidence PNGs

**Files:**
- Create: screenshots/01-project-structure.png through screenshots/13-independent-profile.png

**Interfaces:**
- Consumes the completed project, local Git history, and remote tree.
- Produces exactly 13 PNG files, each 1920x1200, each showing one maximized Ubuntu Terminal window with the user prompt, raw command, and real output.

- [ ] Step 1: Launch each terminal in its own window

Use a separate gnome-terminal window for each capture, maximize it with the window manager, change into the project directory, and execute one evidence command. Use the stock interactive prompt so username, hostname, and directory retain terminal colors.

- [ ] Step 2: Capture required evidence commands

Capture commands for: find project structure; grep semantic landmarks; heading outline; navigation hrefs; image alt; table; form labels; DOM-relevant nested source; corrected debug source; validation result; Git log; remote tree; and profile structure.

- [ ] Step 3: Verify image dimensions

~~~bash
identify -format '%f %wx%h\n' screenshots/*.png
~~~

Expected: 13 lines, all ending in 1920x1200.

### Task 6: Fill the Original Worksheet with UV Python

**Files:**
- Create: CSCE3420_Class_Activity_3_HTML_completed.docx

**Interfaces:**
- Consumes the original worksheet and screenshot PNGs.
- Produces the completed worksheet with identity, answers, explanations, debug table, audit marks, and embedded evidence.

- [ ] Step 1: Map response paragraphs and screenshot tables

Use uv run with python-docx and lxml to identify the original paragraph/table indexes before mutation. Replace only response placeholders and screenshot placeholder cells.

- [ ] Step 2: Fill all written responses

Use concise, scenario-specific answers for all four concept questions, applied checks, path explanation, ordered-list rationale, label investigation, metadata choice, DOM experiment, accessibility decisions, final analysis, outline, and debug correction table. Fill each screenshot explanation with three short lines describing action, result, and evidence.

- [ ] Step 3: Embed all 13 PNGs in matching cells

Remove INSERT SCREENSHOT HERE text, insert the matching PNG, and set only the image width needed to keep the original worksheet readable. Preserve table borders, paragraph styles, and existing page formatting.

- [ ] Step 4: Remove grading-only material

Delete content headed Grading Rubric and TA Grading Guidelines, the rubric table, content headed Grading Rubric, content headed TA Grading Guidelines, and content headed Activity Completion Checklist. Keep Final Submission Requirements and all student-facing activity content.

### Task 7: Verify Final Deliverables

**Files:**
- Verify: CSCE3420_Class_Activity_3_HTML_completed.docx
- Verify: screenshots/*.png
- Verify: Williams_Clyde_CSCE3420_ClassActivity3/*

- [ ] Step 1: Reopen the DOCX with UV Python

Confirm identity values, 13 embedded images, no rubric/guidelines/checklist text, and all source-response sections remain present.

- [ ] Step 2: Render and visually inspect

Convert the completed DOCX to a temporary PDF with LibreOffice and inspect representative pages. Do not replace the DOCX or alter its original styles.

- [ ] Step 3: Verify repository synchronization

Run git status, git ls-remote origin, and git ls-tree -r origin/main to confirm a clean worktree and remote source files.

**Unresolved questions:** None. Remote URL, student data, screenshot resolution, and email identity are specified.
