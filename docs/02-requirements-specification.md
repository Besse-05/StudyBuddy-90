# Requirements Specification: StudyBuddy

**Authors:** Besma Demdoum (6905140030), Elizaveta Marchenko (6905140040) | **Project:** StudyBuddy

## 1. Introduction

### 1.1 Purpose
This document defines the functional and non-functional requirements for **StudyBuddy**, a web-based platform that helps students find affordable peer tutors, join study groups, share study materials, and organize study sessions in one place.

### 1.2 Scope
The requirements cover the MVP with four features: Find a Tutor, Study Groups, Study Materials, and Schedule & Chat.

### 1.3 Definitions

| Term | Meaning |
|---|---|
| Student | A registered user looking for tutoring, groups, or materials |
| Tutor | A registered student who offers tutoring in one or more subjects |
| Admin | A user who manages and moderates the platform |
| Session | A tutoring meeting between a student and a tutor |
| Study group | A group of students who study the same subject together |
| MVP | Minimum Viable Product |

## 2. User Roles

| Role | Description | Main abilities |
|---|---|---|
| **Guest** | Not logged in | View landing page, register, log in |
| **Student** | Registered user | Find tutors, request sessions, join groups, upload and download materials, chat, schedule |
| **Tutor** | Student who offers tutoring (also has all Student abilities) | Manage tutor profile, subjects, prices, availability; accept or decline requests |
| **Admin** | Platform moderator | Manage users, remove inappropriate content, manage subjects |

## 3. Functional Requirements

Priority: **High** = must have in MVP, **Medium** = should have, **Low** = nice to have.

### 3.1 Account Management

| ID | Requirement | Priority |
|---|---|---|
| FR-1 | The system shall allow a user to register with name, email, and password. | High |
| FR-2 | The system shall allow a registered user to log in and log out. | High |
| FR-3 | The system shall allow a user to edit their profile (name, photo, major, bio). | Medium |
| FR-4 | The system shall allow a student to apply to become a tutor by creating a tutor profile. | High |

### 3.2 Feature 1: Find a Tutor

| ID | Requirement | Priority |
|---|---|---|
| FR-5 | The system shall display a list of tutors that can be browsed by subject. | High |
| FR-6 | The system shall allow users to filter tutors by subject, price range, and rating. | Medium |
| FR-7 | The system shall display a tutor profile showing name, photo, bio, subjects, rating, reviews, and hourly price. | High |
| FR-8 | The system shall display each tutor's weekly availability (days and time slots). | High |
| FR-9 | The system shall allow a student to request a tutoring session by choosing a subject, an available time slot, and an optional message. | High |
| FR-10 | The system shall allow a tutor to accept or decline a session request. | High |
| FR-11 | The system shall notify the student when the request is accepted or declined. | High |
| FR-12 | The system shall allow a student to rate and review a tutor after a completed session. | Medium |
| FR-13 | The system shall allow a tutor to add, edit, and remove their subjects, price, and availability. | High |

### 3.3 Feature 2: Study Groups

| ID | Requirement | Priority |
|---|---|---|
| FR-14 | The system shall allow users to search for study groups by subject. | High |
| FR-15 | The system shall display group details: name, subject, description, members, and meeting times. | High |
| FR-16 | The system shall allow a student to join a study group. | High |
| FR-17 | The system shall allow a student to leave a study group they have joined. | High |
| FR-18 | The system shall allow a student to create a new study group with a subject, description, meeting time, and maximum size. | Medium |
| FR-19 | The system shall prevent joining a group that is full. | Medium |
| FR-20 | The system shall allow members of the same group to see each other's names and connect through group chat. | High |

### 3.4 Feature 3: Study Materials

| ID | Requirement | Priority |
|---|---|---|
| FR-21 | The system shall allow users to browse study materials by subject. | High |
| FR-22 | The system shall allow a student to upload notes or study materials (PDF, DOCX, PPTX, images) with a title, subject, and description. | High |
| FR-23 | The system shall allow users to search materials by keyword, title, or subject. | High |
| FR-24 | The system shall allow users to view and download materials. | High |
| FR-25 | The system shall allow users to filter materials by type (notes, past exam, summary, practice questions) to support exam preparation. | Medium |
| FR-26 | The system shall allow an uploader to edit or delete their own materials. | Medium |
| FR-27 | The system shall allow users to report inappropriate materials, and allow Admins to remove them. | Medium |

### 3.5 Feature 4: Schedule & Chat

| ID | Requirement | Priority |
|---|---|---|
| FR-28 | The system shall display a schedule of the user's upcoming tutoring sessions and study group meetings. | High |
| FR-29 | The system shall allow a user to schedule a study session by choosing a date, time, subject, and participants. | High |
| FR-30 | The system shall allow a user to reschedule or cancel a session they created. | Medium |
| FR-31 | The system shall allow one-to-one chat between a student and a tutor. | High |
| FR-32 | The system shall allow group chat among study group members. | High |
| FR-33 | The system shall display the time each message was sent and the sender's name. | Medium |
| FR-34 | The system shall send reminders for upcoming sessions and group meetings (for example 24 hours and 1 hour before). | High |
| FR-35 | The system shall allow a user to turn reminders on or off. | Low |

### 3.6 Administration

| ID | Requirement | Priority |
|---|---|---|
| FR-36 | The system shall allow an Admin to manage the list of subjects. | Medium |
| FR-37 | The system shall allow an Admin to deactivate user accounts. | Medium |
| FR-38 | The system shall allow an Admin to remove reported content. | Medium |

## 4. Non-Functional Requirements

| ID | Category | Requirement |
|---|---|---|
| NFR-1 | Usability | A new user shall be able to find a tutor and request a session within 3 minutes without training. |
| NFR-2 | Usability | The interface shall be clear, consistent, and easy to navigate with a maximum of 3 clicks to reach any main feature. |
| NFR-3 | Responsiveness | The system shall work on desktop, tablet, and mobile browsers. |
| NFR-4 | Performance | Pages shall load within 3 seconds on a normal internet connection. |
| NFR-5 | Performance | Search results shall appear within 2 seconds. |
| NFR-6 | Security | Passwords shall be stored hashed, never as plain text. |
| NFR-7 | Security | The system shall use HTTPS for all communication. |
| NFR-8 | Security | Users shall only access features allowed by their role. |
| NFR-9 | Privacy | The system shall only collect personal data needed for its features and shall not share it with third parties. |
| NFR-10 | Reliability | The system shall be available at least 95% of the time. |
| NFR-11 | Scalability | The system shall support at least 500 registered users in the MVP. |
| NFR-12 | Compatibility | The system shall work on current versions of Chrome, Edge, Firefox, and Safari. |
| NFR-13 | File limits | Uploaded files shall not exceed 20 MB each. |
| NFR-14 | Maintainability | The code and documents shall be stored in version control on GitHub. |

## 5. Constraints and Assumptions

- The MVP is a responsive web application only.
- Payment is not processed in the system. Prices are for information only.
- Users must have a valid student email to register.

## 6. Requirements Traceability (Feature to Requirements)

| Feature | Requirement IDs |
|---|---|
| Account Management | FR-1 to FR-4 |
| Find a Tutor | FR-5 to FR-13 |
| Study Groups | FR-14 to FR-20 |
| Study Materials | FR-21 to FR-27 |
| Schedule & Chat | FR-28 to FR-35 |
| Administration | FR-36 to FR-38 |

## 7. User Stories (Summary)

| ID | As a... | I want to... | So that... |
|---|---|---|---|
| US-1 | Student | browse tutors by subject | I can find help in the subject I struggle with |
| US-2 | Student | see tutor prices and ratings | I can choose an affordable and trusted tutor |
| US-3 | Student | request a session at an available time | I can get tutoring that fits my schedule |
| US-4 | Student | search and join study groups | I can study with classmates |
| US-5 | Student | upload and search notes | I can share and find exam materials |
| US-6 | Student | see my upcoming sessions in one place | I do not miss any study event |
| US-7 | Student | chat with tutors and group members | I can ask questions and coordinate |
| US-8 | Student | receive reminders | I remember my sessions |
| US-9 | Tutor | set my subjects, price, and availability | students can book me |
| US-10 | Tutor | accept or decline requests | I control my own schedule |
| US-11 | Admin | remove inappropriate content | the platform stays safe |
