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
4. Read the log file's entries for today and condense them into a short bullet list (not a raw dump).
5. Check whether today already has a `## <Weekday>, <Month> <Day>` section in the week file:
   - If it doesn't exist yet, append a new section with the condensed bullets.
   - If it already exists, compare bullet-by-bullet and append only the bullets whose content isn't already present under that heading — never re-add a bullet that's already there, and never remove or rewrite existing bullets. If every condensed bullet is already present, make no changes.
6. Update `README.md`'s week list to include this week's file if it isn't already linked there.
7. Run `git status`/`git diff` to check whether anything actually changed. If nothing changed (everything was already present), stop here — don't create an empty commit.
8. Otherwise stage, commit (`git commit -m "Add <date> learning entry"` or `"Start week of <range>"` if the file was just created), and push to `origin`.

## Notes

- Never overwrite a previous day's section — only append genuinely new bullets.
- If `L:\LLM\logs\history-YYYY-MM-DD.txt` doesn't exist for today, this is a no-op, not an error.
- Running this skill multiple times in the same day (e.g. the nightly task firing, then a manual run later) must be safe and produce no duplicate content — always check what's already there before adding anything.
- This skill is meant to be invoked headlessly by a daily scheduled task (Windows Task Scheduler), but also works fine invoked manually via `/weekly-learning-log`.
