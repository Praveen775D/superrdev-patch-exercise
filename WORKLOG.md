# WORKLOG.md

# Full-Stack Patch Exercise - Investigation Log

## Candidate

UDUGUNDLA PRAVEEN

## Date

11 June 2026

---

# Environment Setup

## Backend

Command:

.\mvnw.cmd spring-boot:run

Result:

* Backend started successfully.
* Spring Boot application running on port 8080.
* H2 database initialized successfully.
* API available at http://localhost:8080

Notes:

* Java Version: 21.0.3
* No startup errors found.

---

## Frontend

Commands:

npm install
npm run dev

Result:

* Frontend started successfully.
* Application available at http://localhost:5173

Notes:

* Vite development server running normally.
* Backend proxy connection working.

---

# Initial Smoke Testing

## Search Functionality

Tested Search Terms:

* api
* bug
* frontend

Observation:

* Search returns matching tasks.
* Results appear to update correctly.

Status:

Investigating further.

---

## Status Filter

Tested:

* OPEN
* IN_PROGRESS
* DONE

Observation:

* Filter updates task list.
* Need to verify backend filtering logic.

Status:

Investigating further.

---

## Combined Filters

Tested:

* Search = api
* Status = OPEN

Observation:

* Need to verify if both filters are applied correctly.

Status:

Investigating further.

---

# Console Observations

## Observation 1

Location:

Browser Console

Finding:

Multiple API requests are triggered while typing.

Example:

/api/tasks?q=a&page=1&pageSize=10
/api/tasks?q=ap&page=1&pageSize=10
/api/tasks?q=api&page=1&pageSize=10

Possible Root Cause:

Search input may not be debounced.

Potential Fix:

Implement debounce to reduce unnecessary API calls.

Priority:

Medium

Status:

Under Investigation

---

## Observation 2

Location:

Browser Console

Finding:

favicon.ico returns 404.

Possible Root Cause:

Missing favicon file.

Priority:

Low

Decision:

Likely not worth fixing within assignment timebox.

Status:

Not Planned

---

# Bugs Fixed

(Add entries here as fixes are completed)

## Bug 1

Location:

TBD

Discovery Method:

TBD

Root Cause:

TBD

Fix Applied:

TBD

Reasoning:

TBD

Verification:

TBD

---

# Improvements

(Add improvements here)

## Improvement 1

Description:

TBD

Reason:

TBD

Impact:

TBD

---

# Remaining Risks

(Add after code review)

* TBD

---

# Final Submission Notes

Files Modified:

* TBD

Commits:

* TBD

Handwritten Notes Added:

* Yes / No

NOTES.md Completed:

* Yes / No
