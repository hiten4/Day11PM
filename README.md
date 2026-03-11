# Day11PM
# Exception Handling and Resilient Systems

## Overview
This assignment focuses on improving Python programs by adding proper exception handling, retry logic, logging, and debugging techniques.

---

## Part A — Error Handling Refactor
- Added `try`, `except`, `else`, and `finally` blocks to earlier programs.
- Implemented input validation using `raise`.
- Used specific exceptions instead of `except:`.
- Added logging to one program to record errors in a file.
- Created `error_handling_checklist.md` to document handled exceptions and recovery actions.

---

## Part B — Resilient File Processor
Program: `file_processor_resilient.py`

Features:
- Reads multiple CSV files from a directory.
- Handles corrupted, empty, or invalid files.
- Logs full error tracebacks.
- Implements retry logic for `PermissionError`.
- Waits **1 second** between retries.
- Generates `processing_report.json` containing:
  - files_processed
  - files_failed
  - error_details

---

## Part C — Interview Ready
Topics covered:
- Execution flow of `try`, `except`, `else`, `finally`
- Function `safe_json_load()` with proper error handling
- Debugging and improving faulty exception handling code

---

## Part D — AI-Augmented Task
- Used AI to generate a `@retry` decorator.
- The decorator retries failed functions with exponential backoff.
- Tested with a function that fails randomly.
- Wrote a critical evaluation of the AI-generated solution.

---

## Technologies Used
- Python
- json
- csv
- logging
- traceback
- time module
- decorators
