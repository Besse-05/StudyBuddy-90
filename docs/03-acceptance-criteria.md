# Acceptance Criteria: StudyBuddy

**Authors:** Besma Demdoum (6905140030), Elizaveta Marchenko (6905140040) | **Project:** StudyBuddy

Acceptance criteria are written in **Given / When / Then** format. Each one is linked to a requirement ID from the Requirements Specification (`02-requirements-specification.md`).

A requirement is **accepted** when all of its acceptance criteria pass.

---

## 1. Account Management

### AC-1 Register (FR-1)
- **Given** I am a guest on the registration page,
  **When** I enter a valid name, student email, and password and submit,
  **Then** my account is created and I am logged in.
- **Given** I enter an email that is already registered,
  **When** I submit,
  **Then** I see an error message and no new account is created.
- **Given** I leave a required field empty,
  **When** I submit,
  **Then** the system highlights the missing field and does not register me.

### AC-2 Log in and log out (FR-2)
- **Given** I have an account,
  **When** I enter the correct email and password,
  **Then** I am taken to my dashboard.
- **Given** I enter a wrong password,
  **When** I submit,
  **Then** I see "Invalid email or password" and stay on the login page.
- **Given** I am logged in,
  **When** I click Log out,
  **Then** my session ends and I return to the landing page.

### AC-3 Edit profile (FR-3)
- **Given** I am logged in,
  **When** I change my bio or photo and click Save,
  **Then** the changes are saved and shown on my profile.

### AC-4 Become a tutor (FR-4)
- **Given** I am a logged-in student,
  **When** I fill in my subjects, price, and bio and submit the tutor form,
  **Then** I get a tutor profile and appear in the tutor list.

---

## 2. Feature 1: Find a Tutor

### AC-5 Browse tutors by subject (FR-5)
- **Given** I am on the Find a Tutor page,
  **When** I select the subject "Calculus",
  **Then** only tutors who teach Calculus are shown.
- **Given** no tutors teach the selected subject,
  **When** the list loads,
  **Then** I see the message "No tutors found for this subject."

### AC-6 Filter tutors (FR-6)
- **Given** I am viewing the tutor list,
  **When** I set a maximum price of 300 and a minimum rating of 4,
  **Then** only tutors within the price limit and with a rating of 4 or higher are shown.

### AC-7 View tutor profile (FR-7)
- **Given** I am on the tutor list,
  **When** I click a tutor,
  **Then** I see the tutor's name, photo, bio, subjects, average rating, reviews, and hourly price.

### AC-8 Check availability (FR-8)
- **Given** I am on a tutor's profile,
  **When** I open the availability section,
  **Then** I see the tutor's weekly time slots, and booked slots are marked as unavailable.

### AC-9 Request a session (FR-9)
- **Given** I am logged in and viewing a tutor's profile,
  **When** I choose a subject and an available time slot and click Request Session,
  **Then** a request with status "Pending" is created and the tutor is notified.
- **Given** I try to request a slot that is already booked,
  **When** I submit,
  **Then** the system rejects the request and asks me to choose another slot.

### AC-10 Accept or decline request (FR-10, FR-11)
- **Given** I am a tutor with a pending request,
  **When** I click Accept,
  **Then** the status changes to "Accepted", the slot becomes unavailable, and the student is notified.
- **Given** I am a tutor with a pending request,
  **When** I click Decline,
  **Then** the status changes to "Declined" and the student is notified.

### AC-11 Rate a tutor (FR-12)
- **Given** I have completed a session with a tutor,
  **When** I give a rating from 1 to 5 and an optional review,
  **Then** the rating is saved and the tutor's average rating is updated.
- **Given** I have never had a session with the tutor,
  **When** I view their profile,
  **Then** I cannot submit a rating.

### AC-12 Manage tutor details (FR-13)
- **Given** I am a tutor,
  **When** I add a new subject, change my price, or edit my availability and save,
  **Then** my profile shows the updated information.

---

## 3. Feature 2: Study Groups

### AC-13 Search groups by subject (FR-14)
- **Given** I am on the Study Groups page,
  **When** I search for "Physics",
  **Then** only study groups for Physics are shown.

### AC-14 View group details (FR-15)
- **Given** I click on a study group,
  **When** the details page opens,
  **Then** I see the group name, subject, description, member list, and meeting times.

### AC-15 Join a group (FR-16, FR-19)
- **Given** I am logged in and a group has free places,
  **When** I click Join,
  **Then** I become a member and the group appears in my schedule.
- **Given** a group is full,
  **When** I view the group,
  **Then** the Join button is disabled and shows "Group full".

### AC-16 Leave a group (FR-17)
- **Given** I am a member of a group,
  **When** I click Leave and confirm,
  **Then** I am removed from the member list and the group disappears from my schedule.

### AC-17 Create a group (FR-18)
- **Given** I am logged in,
  **When** I fill in the group name, subject, description, meeting time, and maximum size and submit,
  **Then** the group is created and I am its first member.

### AC-18 Connect with members (FR-20)
- **Given** I am a member of a group,
  **When** I open the group page,
  **Then** I can see all member names and open the group chat.
- **Given** I am not a member,
  **When** I try to open the group chat,
  **Then** access is denied.

---

## 4. Feature 3: Study Materials

### AC-19 Browse materials by subject (FR-21)
- **Given** I am on the Study Materials page,
  **When** I select a subject,
  **Then** only materials for that subject are listed with title, uploader, and date.

### AC-20 Upload materials (FR-22)
- **Given** I am logged in,
  **When** I choose a PDF under 20 MB, enter a title and subject, and click Upload,
  **Then** the file is saved and appears in the materials list.
- **Given** I choose a file larger than 20 MB or an unsupported type,
  **When** I click Upload,
  **Then** I see an error and the file is not uploaded.

### AC-21 Search materials (FR-23)
- **Given** I am on the Study Materials page,
  **When** I type "midterm" in the search box,
  **Then** materials with "midterm" in the title, description, or subject are shown.
- **Given** no material matches,
  **When** the results load,
  **Then** I see "No materials found."

### AC-22 View and download (FR-24)
- **Given** I am viewing a material,
  **When** I click Download,
  **Then** the file downloads to my device.

### AC-23 Filter by type for exam preparation (FR-25)
- **Given** I am on the Study Materials page,
  **When** I filter by "Past exam",
  **Then** only materials marked as past exams are shown.

### AC-24 Edit or delete own material (FR-26)
- **Given** I uploaded a material,
  **When** I click Delete and confirm,
  **Then** the material is removed from the list.
- **Given** I did not upload the material,
  **When** I view it,
  **Then** I do not see Edit or Delete buttons.

### AC-25 Report material (FR-27)
- **Given** I am viewing a material,
  **When** I click Report and give a reason,
  **Then** the report is sent to the Admin.

---

## 5. Feature 4: Schedule & Chat

### AC-26 View schedule (FR-28)
- **Given** I have sessions and group meetings,
  **When** I open the Schedule page,
  **Then** I see all upcoming events sorted by date and time, with type, subject, and participants.
- **Given** I have no upcoming events,
  **When** I open the Schedule page,
  **Then** I see "No upcoming sessions."

### AC-27 Schedule a session (FR-29)
- **Given** I am logged in,
  **When** I choose a date, time, subject, and participants and click Save,
  **Then** the session is added to the schedule of everyone involved.
- **Given** I choose a time in the past,
  **When** I click Save,
  **Then** the system shows an error and does not create the session.

### AC-28 Reschedule or cancel (FR-30)
- **Given** I created a session,
  **When** I change the time or click Cancel,
  **Then** the session is updated or removed and participants are notified.

### AC-29 One-to-one chat (FR-31, FR-33)
- **Given** I have a conversation with a tutor,
  **When** I type a message and press Send,
  **Then** the message appears in the chat with my name and the time sent, and the tutor can see it.

### AC-30 Group chat (FR-32)
- **Given** I am a member of a study group,
  **When** I send a message in the group chat,
  **Then** all group members can see it.

### AC-31 Reminders (FR-34, FR-35)
- **Given** I have a session in 24 hours and reminders are on,
  **When** the reminder time is reached,
  **Then** I receive a reminder with the subject, date, and time.
- **Given** I turned reminders off,
  **When** a session approaches,
  **Then** I do not receive reminders.

---

## 6. Administration

### AC-32 Manage subjects (FR-36)
- **Given** I am an Admin,
  **When** I add or rename a subject,
  **Then** the subject list updates and is available in all filters.

### AC-33 Deactivate account (FR-37)
- **Given** I am an Admin,
  **When** I deactivate a user,
  **Then** that user can no longer log in.

### AC-34 Remove reported content (FR-38)
- **Given** I am an Admin viewing a reported material,
  **When** I click Remove,
  **Then** the material is no longer visible to users.

---

## 7. Non-Functional Acceptance Criteria

| ID | Related NFR | Criteria |
|---|---|---|
| AC-NFR-1 | NFR-3 | **Given** I open the site on a phone, tablet, or desktop, **Then** all pages display correctly without horizontal scrolling. |
| AC-NFR-2 | NFR-4 | **Given** a normal internet connection, **When** any main page loads, **Then** it loads in 3 seconds or less. |
| AC-NFR-3 | NFR-6 | **Given** the database, **When** I inspect the password column, **Then** passwords are stored as hashes. |
| AC-NFR-4 | NFR-8 | **Given** I am a Student, **When** I try to open an Admin page, **Then** access is denied. |
| AC-NFR-5 | NFR-1 | **Given** a first-time user, **When** they try to request a tutor session, **Then** they complete it within 3 minutes without help. |
