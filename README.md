# Module 1 – Authentication & Identity Management

**EduOS** | Final Year Project

Complete PostgreSQL database schema for **Module 1: Authentication & Identity Management** of the EduOS platform.

---

## Overview

This module serves as the foundation of EduOS. It manages user identity, authentication, authorization, session handling, and profile extensions for Students, Faculty, and Admins in a multi-tenant environment.

---

## Features

- Multi-tenant architecture (Institution-level isolation)
- Hierarchical Role-Based Access Control (RBAC)
- Attribute-Based Access Control (ABAC) support via JSONB conditions
- Granular permissions (`module:resource:action`)
- Multi-Factor Authentication (MFA) ready
- Secure session management with device fingerprinting & risk scoring
- Immutable & partitioned login history
- Soft deletes + Optimistic locking
- 1:1 Profile extensions (Student, Faculty, Admin)

---

## Database Entities

| #  | Table               | Purpose                                      |
|----|---------------------|----------------------------------------------|
| 1  | `users`             | Core identity & authentication root          |
| 2  | `roles`             | Hierarchical role definitions                |
| 3  | `permissions`       | Atomic permission rules                      |
| 4  | `role_permissions`  | Role ↔ Permission mapping (ALLOW/DENY + ABAC)|
| 5  | `user_roles`        | User ↔ Role assignments                      |
| 6  | `auth_providers`    | Password / OAuth / SAML providers            |
| 7  | `user_sessions`     | Active refresh token sessions                |
| 8  | `login_history`     | Immutable authentication event log           |
| 9  | `student_profiles`  | Academic profile for students                |
| 10 | `faculty_profiles`  | Professional profile for faculty             |
| 11 | `admin_profiles`    | Administrative profile for admins            |

---

## Tech Stack

- **Database**: PostgreSQL 16+
- **Primary Keys**: UUIDv7 (time-ordered)
- **Search**: Full-text search using `tsvector` + GIN index
- **Special Types**: `INET`, `JSONB`, `POINT`, Custom Enums

---

## Project Structure

```bash
module-1-eduos/
├── schema/
│   ├── 01_enums.sql
│   ├── 02_tables.sql
│   ├── 03_constraints.sql
│   ├── 04_indexes.sql
│   └── 05_triggers.sql
├── docs/
│   └── schema-design.md
├── seeds/
└── README.md
