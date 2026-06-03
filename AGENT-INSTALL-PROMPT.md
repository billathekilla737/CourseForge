# Agent install prompt (for less-techy instructors)

Have your colleague save the file `notion-to-canvas-skill.zip` (the one you email
them) into their **Downloads** folder, open **Claude Code**, and paste the prompt
below. Their own agent will install the skill for them.

> Works in **Claude Code** only (it needs file + shell access). It does **not** work
> in the claude.ai website. After it finishes, they must fully restart Claude Code.

---

## Copy everything between the lines and paste it into Claude Code

```
You are installing a Claude Code skill called "notion-to-canvas" on THIS computer for
me. Work carefully, explain each step in plain language, and stop and ask if anything
is unclear. I may be non-technical.

GOAL: finish with the skill installed so that this file exists:
  - Windows:      C:\Users\<MY-USERNAME>\.claude\skills\notion-to-canvas\SKILL.md
  - macOS/Linux:  ~/.claude/skills/notion-to-canvas/SKILL.md

STEP 1 - Find the source. Look, in this order:
  (a) A zip named "notion-to-canvas-skill.zip" - search my Downloads, Desktop, and the
      current folder.
  (b) An already-extracted folder named "notion-to-canvas" that contains a SKILL.md.
  (c) Only if I clearly have git installed AND access to the repo, you may instead run:
      git clone https://github.com/billathekilla737/garris-canvas-tools.git
      and use the folder: plugins/notion-to-canvas/skills/notion-to-canvas
  (d) If you find none of these, STOP and tell me exactly:
      "I can't find notion-to-canvas-skill.zip. Please save the file your colleague
       emailed you into your Downloads folder, then run this prompt again."
  Do NOT invent or hand-write the skill's contents. Use the real files only.

STEP 2 - Extract (if it was a zip). Unzip it to a temporary folder. Then locate the
  folder that DIRECTLY contains SKILL.md (it should be named "notion-to-canvas").
  Watch out for double-nesting like notion-to-canvas/notion-to-canvas - you want the
  one that actually has SKILL.md plus the "references" and "scripts" subfolders.

STEP 3 - Install. Create the folder ~/.claude/skills if it does not exist. Copy the
  whole "notion-to-canvas" folder (with its references/ and scripts/ subfolders) into
  ~/.claude/skills, replacing any older copy that may be there.

STEP 4 - Verify. Confirm that SKILL.md now exists at the target path above, and that
  the references/ and scripts/ subfolders came along. Show me the final folder listing
  so I can see it worked.

STEP 5 - Report. Tell me it is installed, and that I must FULLY CLOSE and reopen Claude
  Code for it to load. After I restart, I can test by asking: "Do you have the
  notion-to-canvas skill?"

IMPORTANT RULES:
  - Do NOT ask me for, or set up, any Canvas token, password, or course settings right
    now. This task ONLY installs the skill. Token setup happens later in a separate
    course-work folder.
  - Do NOT change anything outside ~/.claude/skills/notion-to-canvas.
  - It is normal for you to ask my permission to run a command or write a file -
    I will approve those.
```

---

After install + restart, the instructor sets up their Canvas token in a course-work
folder (the skill or the PDF guide walks them through that part).
