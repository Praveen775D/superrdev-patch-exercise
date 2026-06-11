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

## Bug #1

Location:
TaskRepository.java

Discovery:
Reviewed repository query after testing search and filter behavior.

Root Cause:
SQL query used AND and OR without parentheses. SQL operator precedence caused filters to be applied inconsistently.

Impact:
Status filtering and archived filtering could return incorrect search results.

Fix:
Grouped title and description search conditions using parentheses.

Verification:
Confirmed search and status filters now apply consistently across all matching tasks.

Priority:
High

## Bug #2

Location:
TaskController.java

Discovery:
Search requests felt unusually slow during testing.

Root Cause:
The controller intentionally delayed every request using Thread.sleep() based on query length.

Impact:
Search became slower as users typed, causing poor user experience and unnecessary server blocking.

Fix:
Removed artificial delay logic and related complexity calculations.

Verification:
Search results now return immediately without unnecessary waiting.

Priority:
High

---

## Bug #3

Location:
TaskController.java

Discovery:
Reviewed status parsing logic while investigating potential HTTP 500 errors.

Root Cause:
TaskStatus.valueOf() throws IllegalArgumentException when an invalid status value is supplied.

Impact:
Invalid user input could cause a server error.

Fix:
Added validation and returned HTTP 400 for invalid status values.

Verification:
Invalid status requests now return a controlled error response.

Priority:
Medium

# Bug #4

Location:
useTasks.jsx

Issue:
Loading state not reset after failure.

Root Cause:
setLoading(false) missing in error path.

Fix:
Used finally() and reset errors before requests.

Result:
Stable loading/error handling.

# Bug #5

Location:
App.jsx

Issue:
Pagination stayed on old page after filtering.

Root Cause:
Page state not reset.

Fix:
Reset page to 1 when query or status changes.

Result:
Correct search and filter behavior.