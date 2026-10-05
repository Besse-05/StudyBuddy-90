# Database Design: StudyBuddy

**Authors:** Besma Demdoum (6905140030), Elizaveta Marchenko (6905140040) | **Project:** StudyBuddy

## 1. Overview

This document describes the relational database for StudyBuddy. It supports all four MVP features: Find a Tutor, Study Groups, Study Materials, and Schedule & Chat.

- **Database type:** Relational (SQL, for example PostgreSQL or MySQL)
- **Naming rules:** table names in plural `snake_case`; primary keys are `id`
- **Keys:** PK = Primary Key, FK = Foreign Key, UQ = Unique

## 2. Entity Relationship Diagram

```mermaid
erDiagram
    USERS ||--o| TUTOR_PROFILES : "may have"
    TUTOR_PROFILES ||--o{ TUTOR_SUBJECTS : "teaches"
    SUBJECTS ||--o{ TUTOR_SUBJECTS : "taught in"
    TUTOR_PROFILES ||--o{ AVAILABILITY_SLOTS : "offers"
    USERS ||--o{ SESSION_REQUESTS : "requests"
    TUTOR_PROFILES ||--o{ SESSION_REQUESTS : "receives"
    SUBJECTS ||--o{ SESSION_REQUESTS : "for"
    AVAILABILITY_SLOTS ||--o{ SESSION_REQUESTS : "booked by"
    SESSION_REQUESTS ||--o| RATINGS : "reviewed in"
    USERS ||--o{ RATINGS : "writes"
    SUBJECTS ||--o{ STUDY_GROUPS : "focus of"
    USERS ||--o{ STUDY_GROUPS : "creates"
    STUDY_GROUPS ||--o{ GROUP_MEMBERS : "has"
    USERS ||--o{ GROUP_MEMBERS : "joins"
    SUBJECTS ||--o{ MATERIALS : "categorizes"
    USERS ||--o{ MATERIALS : "uploads"
    MATERIALS ||--o{ MATERIAL_REPORTS : "reported in"
    USERS ||--o{ MATERIAL_REPORTS : "files"
    USERS ||--o{ MESSAGES : "sends"
    STUDY_GROUPS ||--o{ MESSAGES : "contains"
    USERS ||--o{ STUDY_EVENTS : "creates"
    STUDY_GROUPS ||--o{ STUDY_EVENTS : "has"
    STUDY_EVENTS ||--o{ EVENT_PARTICIPANTS : "includes"
    USERS ||--o{ EVENT_PARTICIPANTS : "attends"
    STUDY_EVENTS ||--o{ REMINDERS : "triggers"
    USERS ||--o{ REMINDERS : "receives"

    USERS {
        int id PK
        string full_name
        string email UQ
        string password_hash
        string role
        string major
        string bio
        string photo_url
        boolean is_active
        boolean reminders_enabled
        datetime created_at
    }
    TUTOR_PROFILES {
        int id PK
        int user_id FK
        string headline
        decimal hourly_price
        decimal avg_rating
        int total_reviews
        boolean is_approved
    }
    SUBJECTS {
        int id PK
        string name UQ
        string category
    }
    TUTOR_SUBJECTS {
        int tutor_id FK
        int subject_id FK
    }
    AVAILABILITY_SLOTS {
        int id PK
        int tutor_id FK
        string day_of_week
        time start_time
        time end_time
        boolean is_booked
    }
    SESSION_REQUESTS {
        int id PK
        int student_id FK
        int tutor_id FK
        int subject_id FK
        int slot_id FK
        string message
        string status
        datetime created_at
    }
    RATINGS {
        int id PK
        int session_request_id FK
        int student_id FK
        int tutor_id FK
        int score
        string review
        datetime created_at
    }
    STUDY_GROUPS {
        int id PK
        int subject_id FK
        int created_by FK
        string name
        string description
        string meeting_day
        time meeting_time
        string location
        int max_members
        datetime created_at
    }
    GROUP_MEMBERS {
        int group_id FK
        int user_id FK
        datetime joined_at
    }
    MATERIALS {
        int id PK
        int uploader_id FK
        int subject_id FK
        string title
        string description
        string material_type
        string file_url
        string file_type
        int file_size_kb
        int download_count
        string status
        datetime uploaded_at
    }
    MATERIAL_REPORTS {
        int id PK
        int material_id FK
        int reporter_id FK
        string reason
        string status
        datetime created_at
    }
    MESSAGES {
        int id PK
        int sender_id FK
        int recipient_id FK
        int group_id FK
        string content
        datetime sent_at
        boolean is_read
    }
    STUDY_EVENTS {
        int id PK
        int created_by FK
        int group_id FK
        int session_request_id FK
        string title
        string event_type
        datetime start_datetime
        datetime end_datetime
        string location
        string status
    }
    EVENT_PARTICIPANTS {
        int event_id FK
        int user_id FK
    }
    REMINDERS {
        int id PK
        int event_id FK
        int user_id FK
        datetime remind_at
        boolean is_sent
    }
```

## 3. Table Definitions

### 3.1 users
Stores all accounts (students, tutors, admins).

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | Auto increment |
| full_name | VARCHAR(100) | | Required |
| email | VARCHAR(150) | UQ | Required, student email |
| password_hash | VARCHAR(255) | | Hashed password |
| role | VARCHAR(20) | | `student`, `tutor`, or `admin` |
| major | VARCHAR(100) | | Optional |
| bio | TEXT | | Optional |
| photo_url | VARCHAR(255) | | Optional |
| is_active | BOOLEAN | | Default true; false = deactivated |
| reminders_enabled | BOOLEAN | | Default true |
| created_at | DATETIME | | Default current time |

### 3.2 tutor_profiles
Extra information for users who are tutors.

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | |
| user_id | INT | FK, UQ | References users(id) |
| headline | VARCHAR(150) | | Short intro |
| hourly_price | DECIMAL(8,2) | | Price per hour |
| avg_rating | DECIMAL(2,1) | | Calculated from ratings |
| total_reviews | INT | | Default 0 |
| is_approved | BOOLEAN | | Admin approval if required |

### 3.3 subjects
List of subjects.

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | |
| name | VARCHAR(100) | UQ | For example "Calculus" |
| category | VARCHAR(100) | | For example "Mathematics" |

### 3.4 tutor_subjects
Links tutors and subjects (many-to-many).

| Column | Type | Key | Notes |
|---|---|---|---|
| tutor_id | INT | PK, FK | References tutor_profiles(id) |
| subject_id | INT | PK, FK | References subjects(id) |

### 3.5 availability_slots
Weekly time slots offered by tutors.

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | |
| tutor_id | INT | FK | References tutor_profiles(id) |
| day_of_week | VARCHAR(10) | | Monday to Sunday |
| start_time | TIME | | |
| end_time | TIME | | Must be after start_time |
| is_booked | BOOLEAN | | Default false |

### 3.6 session_requests
Tutoring session requests.

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | |
| student_id | INT | FK | References users(id) |
| tutor_id | INT | FK | References tutor_profiles(id) |
| subject_id | INT | FK | References subjects(id) |
| slot_id | INT | FK | References availability_slots(id) |
| message | TEXT | | Optional note from student |
| status | VARCHAR(20) | | `pending`, `accepted`, `declined`, `completed`, `cancelled` |
| created_at | DATETIME | | |

### 3.7 ratings
Reviews of tutors after completed sessions.

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | |
| session_request_id | INT | FK, UQ | One rating per session |
| student_id | INT | FK | References users(id) |
| tutor_id | INT | FK | References tutor_profiles(id) |
| score | INT | | 1 to 5 |
| review | TEXT | | Optional |
| created_at | DATETIME | | |

### 3.8 study_groups

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | |
| subject_id | INT | FK | References subjects(id) |
| created_by | INT | FK | References users(id) |
| name | VARCHAR(100) | | |
| description | TEXT | | |
| meeting_day | VARCHAR(10) | | |
| meeting_time | TIME | | |
| location | VARCHAR(150) | | Room or online link |
| max_members | INT | | Used to block joining when full |
| created_at | DATETIME | | |

### 3.9 group_members
Links students and groups (many-to-many).

| Column | Type | Key | Notes |
|---|---|---|---|
| group_id | INT | PK, FK | References study_groups(id) |
| user_id | INT | PK, FK | References users(id) |
| joined_at | DATETIME | | |

### 3.10 materials

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | |
| uploader_id | INT | FK | References users(id) |
| subject_id | INT | FK | References subjects(id) |
| title | VARCHAR(150) | | |
| description | TEXT | | |
| material_type | VARCHAR(30) | | `notes`, `past_exam`, `summary`, `practice` |
| file_url | VARCHAR(255) | | Storage location |
| file_type | VARCHAR(20) | | pdf, docx, pptx, png, jpg |
| file_size_kb | INT | | Max 20480 (20 MB) |
| download_count | INT | | Default 0 |
| status | VARCHAR(20) | | `active` or `removed` |
| uploaded_at | DATETIME | | |

### 3.11 material_reports

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | |
| material_id | INT | FK | References materials(id) |
| reporter_id | INT | FK | References users(id) |
| reason | TEXT | | |
| status | VARCHAR(20) | | `open` or `resolved` |
| created_at | DATETIME | | |

### 3.12 messages
Handles both one-to-one chat and group chat.

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | |
| sender_id | INT | FK | References users(id) |
| recipient_id | INT | FK | References users(id); NULL for group messages |
| group_id | INT | FK | References study_groups(id); NULL for direct messages |
| content | TEXT | | |
| sent_at | DATETIME | | |
| is_read | BOOLEAN | | Default false |

> Rule: exactly one of `recipient_id` or `group_id` must be filled.

### 3.13 study_events
Scheduled tutoring sessions and group meetings shown in the schedule.

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | |
| created_by | INT | FK | References users(id) |
| group_id | INT | FK | NULL if not a group event |
| session_request_id | INT | FK | NULL if not from a tutor request |
| title | VARCHAR(150) | | |
| event_type | VARCHAR(20) | | `tutoring`, `group`, `personal` |
| start_datetime | DATETIME | | |
| end_datetime | DATETIME | | |
| location | VARCHAR(150) | | |
| status | VARCHAR(20) | | `scheduled`, `cancelled`, `completed` |

### 3.14 event_participants

| Column | Type | Key | Notes |
|---|---|---|---|
| event_id | INT | PK, FK | References study_events(id) |
| user_id | INT | PK, FK | References users(id) |

### 3.15 reminders

| Column | Type | Key | Notes |
|---|---|---|---|
| id | INT | PK | |
| event_id | INT | FK | References study_events(id) |
| user_id | INT | FK | References users(id) |
| remind_at | DATETIME | | For example 24h or 1h before event |
| is_sent | BOOLEAN | | Default false |

## 4. Relationships Summary

| Relationship | Type |
|---|---|
| users to tutor_profiles | One to zero-or-one |
| tutor_profiles to subjects (via tutor_subjects) | Many to many |
| tutor_profiles to availability_slots | One to many |
| users to session_requests (as student) | One to many |
| tutor_profiles to session_requests | One to many |
| session_requests to ratings | One to zero-or-one |
| study_groups to users (via group_members) | Many to many |
| subjects to study_groups | One to many |
| subjects to materials | One to many |
| users to materials (uploader) | One to many |
| users to messages (sender) | One to many |
| study_groups to messages | One to many |
| study_events to users (via event_participants) | Many to many |
| study_events to reminders | One to many |

## 5. Requirement Coverage

| Requirements | Tables used |
|---|---|
| FR-1 to FR-4 | users, tutor_profiles |
| FR-5 to FR-13 (Find a Tutor) | tutor_profiles, subjects, tutor_subjects, availability_slots, session_requests, ratings |
| FR-14 to FR-20 (Study Groups) | study_groups, group_members, subjects |
| FR-21 to FR-27 (Study Materials) | materials, material_reports, subjects |
| FR-28 to FR-35 (Schedule & Chat) | study_events, event_participants, messages, reminders |
| FR-36 to FR-38 (Admin) | subjects, users, materials, material_reports |

## 6. Business Rules and Constraints

1. A user's email must be unique.
2. `hourly_price` must be zero or higher.
3. A rating `score` must be between 1 and 5.
4. A student can rate a tutor only once per completed session.
5. An availability slot can be booked by only one accepted request.
6. A student cannot join a group when `COUNT(group_members) >= max_members`.
7. A user can join the same group only once (composite primary key).
8. Uploaded files must be 20 MB or smaller.
9. Deleting a user should deactivate (`is_active = false`) instead of removing data.
10. Deleting a group removes its memberships (cascade).

## 7. Suggested Indexes (for performance)

| Table | Index | Reason |
|---|---|---|
| users | `email` | Fast login |
| tutor_subjects | `subject_id` | Browse tutors by subject |
| study_groups | `subject_id` | Search groups by subject |
| materials | `subject_id`, `title` | Browse and search materials |
| messages | `group_id`, `sent_at` | Load group chat |
| study_events | `start_datetime` | Upcoming schedule |
| reminders | `remind_at`, `is_sent` | Find reminders to send |
