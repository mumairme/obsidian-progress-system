# Progress Dashboard

This dashboard reads your daily notes from `Daily/` using Dataview.

## Daily Input Rule

Open today's daily note and fill the `Daily Progress Input` fields. Use `0` if you did not do something.

## Recent Daily Progress

```dataview
TABLE
  progress_score AS "Score",
  study_minutes AS "Study",
  ai_minutes AS "AI",
  cybersecurity_minutes AS "Cyber",
  language_minutes AS "Language",
  sat_questions AS "SAT Qs",
  exercise_minutes AS "Exercise",
  walk_minutes AS "Walk",
  project_minutes AS "Projects",
  study_abroad_minutes AS "Study Abroad"
FROM "Daily"
SORT file.name DESC
LIMIT 14
```

## Total Progress

```dataview
TABLE WITHOUT ID
  sum(rows.study_minutes) AS "Study",
  sum(rows.ai_minutes) AS "AI",
  sum(rows.cybersecurity_minutes) AS "Cyber",
  sum(rows.language_minutes) AS "Language",
  sum(rows.sat_questions) AS "SAT Qs",
  sum(rows.exercise_minutes) AS "Exercise",
  sum(rows.walk_minutes) AS "Walk",
  sum(rows.project_minutes) AS "Projects",
  sum(rows.study_abroad_minutes) AS "Study Abroad"
FROM "Daily"
GROUP BY "All Time" AS "Progress"
```

## Average Score

```dataview
TABLE WITHOUT ID
  round(average(rows.progress_score), 2) AS "Average Progress Score"
FROM "Daily"
WHERE progress_score > 0
GROUP BY "All Time" AS "Progress"
```

## This Week

Update the date filter when needed.

```dataview
TABLE
  progress_score AS "Score",
  study_minutes AS "Study",
  ai_minutes AS "AI",
  cybersecurity_minutes AS "Cyber",
  language_minutes AS "Language",
  sat_questions AS "SAT Qs",
  project_minutes AS "Projects"
FROM "Daily"
WHERE file.name >= "2026-04-27" AND file.name <= "2026-05-03"
SORT file.name ASC
```

## Progress Questions

- Am I showing up more often?
- Which area is growing?
- Which area keeps getting ignored?
- What is the smallest daily action that would restart momentum?

## Related

- [[Task System]]
- [[Example Weekly Review]]
- [[Daily Checklist Template]]
