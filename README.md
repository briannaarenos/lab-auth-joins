# Lab-Auth-Joins
This module adds reporting endpoints under `/api/reports` using different types of SQL JOINs.


## JOIN Explanations

- **Users with Profiles — LEFT JOIN**  
  Shows all users with their profile information (phone, city, country). Users without profiles still appear, but profile fields are `null`.

- **Roles Right Join — RIGHT JOIN**  
  Returns all roles, even if no users are assigned to them. Ensures no role is excluded.

- **Profiles Full Outer — FULL OUTER JOIN (simulated via UNION)**  
  Returns all users and all profiles, combining both matched and unmatched rows.

- **User-Role Combos — CROSS JOIN**  
  Returns every possible combination of users and roles (Cartesian product).

- **Referrals — SELF JOIN**  
  Shows which users referred other users by joining the users table to itself.

- **Latest Login — Aggregation / Subquery**  
  Returns each user’s most recent login activity, using `MAX(login_time)` per user.

---

## `/api/reports` Endpoints

| Endpoint                                | Method | Purpose |
|-----------------------------------------|--------|---------|
| `/api/reports/users-with-profiles`      | GET    | Show users with their profile details. LEFT JOIN was used. |
| `/api/reports/roles-right-join`         | GET    | Show all roles and their assigned users (if any). RIGHT JOIN was used. |
| `/api/reports/profiles-full-outer`      | GET    | Show all users and all profiles, matched or not. FULL OUTER JOIN (via UNION) was used. |
| `/api/reports/user-role-combos`         | GET    | Show every possible user-role pairing. CROSS JOIN was used. |
| `/api/reports/referrals`                | GET    | Show referral relationships between users. SELF JOIN was used. |
| `/api/reports/latest-login`             | GET    | Show each user’s most recent login timestamp. Aggregation / Subquery was used. |

---

## Authorization

All `/api/reports` endpoints require a **Bearer Token**.  
- ✅ **Positive test**: Call endpoint with a valid token → returns data.  
- ❌ **Negative test**: Call endpoint without/with invalid token → returns an error (`missing bearer token` or `invalid/expired token`).  
