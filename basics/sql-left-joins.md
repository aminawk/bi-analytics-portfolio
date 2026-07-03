# Left Joining data on Metadata (Real-World Notes)

## Overview

In my BI and analytics work, I primarily work with metadata-driven and reporting datasets where a main business entity (projects, customers, portfolios) is enriched using supporting systems such as:

- Time reporting systems
- Financial / budget systems
- HR / resource systems
- Operational metadata tables

Because of this structure, LEFT JOINs are the most commonly used join type in my day-to-day work.

---

## LEFT JOIN (Most Common Pattern)

### Use Case
Return all projects and enrich with time reporting data where available.

```sql
SELECT
    p.project_id,
    p.project_name,
    t.logged_hours
FROM project_metadata p
LEFT JOIN time_reporting t
    ON p.project_id = t.project_id;
