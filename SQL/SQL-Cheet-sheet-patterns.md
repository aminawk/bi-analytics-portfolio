📘 SQL Pattern Cheat Sheet (Interview Style)
1. FILTER rows (simple condition)
❓ Question

Return all users who use Python.

SELECT *
FROM candidates
WHERE skill = 'Python';
2. MULTIPLE VALUES filter
❓ Question

Return users with Python, Tableau, or SQL skills.

SELECT *
FROM candidates
WHERE skill IN ('Python', 'Tableau', 'SQL');
3. COUNT per group
❓ Question

Count users per skill.

SELECT skill, COUNT(*) AS total_users
FROM candidates
GROUP BY skill;
4. "HAS ALL SKILLS" problem (VERY IMPORTANT)
❓ Question

Find candidates who have Python, Tableau, AND SQL.

SELECT candidate_id
FROM candidates
WHERE skill IN ('Python', 'Tableau', 'SQL')
GROUP BY candidate_id
HAVING COUNT(DISTINCT skill) = 3;
5. MAX per group
❓ Question

Find highest salary per department.

SELECT department, MAX(salary) AS max_salary
FROM employees
GROUP BY department;
6. DIFFERENCE between two groups
❓ Question

Difference between max salary in Marketing and Engineering.

SELECT
    ABS(
        MAX(CASE WHEN department = 'marketing' THEN salary END)
        -
        MAX(CASE WHEN department = 'engineering' THEN salary END)
    ) AS salary_difference
FROM employees;
7. ROWS → CATEGORY SPLIT (CASE WHEN)
❓ Question

Count laptop vs mobile users.

SELECT
    COUNT(CASE WHEN device = 'laptop' THEN user_id END) AS laptop_users,
    COUNT(CASE WHEN device = 'mobile' THEN user_id END) AS mobile_users
FROM sessions;
8. DISTINCT users per category
❓ Question

How many unique users used each device?

SELECT
    COUNT(DISTINCT CASE WHEN device = 'laptop' THEN user_id END) AS laptop_users,
    COUNT(DISTINCT CASE WHEN device = 'mobile' THEN user_id END) AS mobile_users
FROM sessions;
9. USERS who satisfy BOTH conditions
❓ Question

Users who used both laptop AND mobile.

SELECT user_id
FROM sessions
GROUP BY user_id
HAVING
    COUNT(DISTINCT CASE WHEN device = 'laptop' THEN 1 END) > 0
AND COUNT(DISTINCT CASE WHEN device = 'mobile' THEN 1 END) > 0;
10. PERCENTAGE of group
❓ Question

Percentage of users who used both devices.

WITH user_flags AS (
    SELECT user_id
    FROM sessions
    GROUP BY user_id
    HAVING
        COUNT(DISTINCT CASE WHEN device = 'laptop' THEN 1 END) > 0
    AND COUNT(DISTINCT CASE WHEN device = 'mobile' THEN 1 END) > 0
)

SELECT
    100.0 * COUNT(*) / (SELECT COUNT(DISTINCT user_id) FROM sessions) AS percentage
FROM user_flags;
🔥 Core Patterns to Memorize
1. Row filtering

→ WHERE

2. Category filtering (multiple values)

→ IN

3. One row per entity

→ GROUP BY

4. “HAS ALL X”

→ GROUP BY + HAVING COUNT(...)

5. “Compare two groups”

→ MAX(CASE WHEN ...)

6. “Split categories”

→ CASE WHEN

7. “Percentage”

→ CTE + COUNT / total

🧠 Mental model (important)

When you see a question, ask:

👉 “Am I working with rows or groups?”
rows → WHERE
groups → GROUP BY
conditional groups → CASE WHEN + aggregation
