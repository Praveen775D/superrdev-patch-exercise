# NOTES

## Summary of Changes

I focused on fixing issues that had the highest impact on correctness, performance, and user experience.

* Fixed a SQL query precedence issue in `TaskRepository` where mixed `AND`/`OR` conditions could return incorrect search results and apply filters inconsistently.
* Removed artificial request latency from `TaskController` that was delaying API responses based on search input length.
* Added validation for invalid status values and return a `400 Bad Request` response instead of allowing an unhandled exception to cause a `500 Internal Server Error`.
* Improved frontend request handling in `useTasks` by ensuring loading state is always cleared and previous errors are reset before new requests.
* Reset pagination when search or status filters change so users do not land on empty pages after filtering.

## What I Chose Not To Change

I considered adding request debouncing for the search input to reduce API calls while typing. However, I treated it as an enhancement rather than a critical bug fix and prioritized correctness, stability, and user experience improvements within the timebox.

## Biggest Remaining Risk

Pagination is currently performed in memory after loading all matching records from the database. While acceptable for small datasets, this approach may become inefficient as data volume grows. Database-level pagination would be a better long-term solution.

## AI Usage

I used ChatGPT to assist with code review, bug identification, root-cause analysis, and validation of potential fixes. All changes were implemented, tested, and reviewed manually to ensure I understood their behavior and impact.
