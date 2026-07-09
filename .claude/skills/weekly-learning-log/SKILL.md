---
name: weekly-learning-log
description: Copies today's entry from the local daily-history-log (L:\LLM\logs\history-YYYY-MM-DD.txt) into this week's file under weeks/, creating the week file if it doesn't exist yet, then commits and pushes. Use for the nightly automated learning-log update.
---

# Weekly Learning Log

Purpose: keep one file per calendar week (Monday–Sunday) in this repo, with a dated section per day, sourced from the local daily-history-log files.

## Steps

1. Determine today's date and the Monday–Sunday range it falls in.
2. The week file is `weeks/YYYY-MM-DD-to-YYYY-MM-DD.md` (Monday's date to Sunday's date).
   - If it doesn't exist, create it with a header: `# Week of <Month> <Day> – <Month> <Day>, <Year>`.
3. Look for `L:\LLM\logs\history-YYYY-MM-DD.txt` (today's date). If it doesn't exist, stop — there's nothing to log today, do not create an empty or placeholder entry.
4. If it exists and today's date doesn't already have a section in the week file:
   - Read the log file's entries for today.
   - Condense them into a short bullet list (not a raw dump) under a new section: `## <Weekday>, <Month> <Day>`.
   - Append that section to the week file.
5. If today's date already has a section in the week file, do nothing (avoid duplicate entries) — the task may run more than once in a day.
6. Update `README.md`'s week list to include this week's file if it isn't already linked there.
7. Stage, commit (`git commit -m "Add <date> learning entry"` or `"Start week of <range>"` if the file was just created), and push to `origin`.

## Notes

- Never overwrite a previous day's section — only append.
- If `L:\LLM\logs\history-YYYY-MM-DD.txt` doesn't exist for today, this is a no-op, not an error.
- This skill is meant to be invoked headlessly by a daily scheduled task (Windows Task Scheduler), but also works fine invoked manually via `/weekly-learning-log`.
