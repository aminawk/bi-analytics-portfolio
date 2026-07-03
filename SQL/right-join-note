# SQL JOIN Strategy in BI (Real-World Usage)

## Overview

In my Business Intelligence work, I operate within a dimensional modelling structure where:

- **Fact tables** contain measurable business events (e.g. budgets, costs, hours)
- **Dimension tables** contain descriptive context (e.g. projects, statuses, business users)

Most reporting use cases require preserving a primary business entity (either fact- or dimension-driven depending on the analysis) and enriching it with supporting datasets from other systems.

In practice, I predominantly use **LEFT JOINs** to maintain consistency and readability across analytical workflows.

However, in Power BI modelling contexts, fact tables often act as the central starting point of analysis due to relationship structures. In some legacy or tool-generated SQL, I have also observed **RIGHT JOINs**, particularly when ensuring completeness of dimension-led views (e.g. project status coverage). In these cases, I typically standardise the logic by converting RIGHT JOINs into equivalent LEFT JOINs for consistency and maintainability.

---

## LEFT JOIN (Primary Pattern in BI Work)

LEFT JOIN is the most commonly used join type in my work, as it ensures the primary dataset is always preserved while allowing enrichment from secondary systems.

### Example Use Case
Return all projects and include budget information where available.

```sql
SELECT
    d.project_id,
    d.project_name,
    f.budget_amount
FROM dim_project d
LEFT JOIN fact_project_budget f
    ON d.project_id = f.project_id;
