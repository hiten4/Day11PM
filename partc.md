# Part C — Interview Ready

## Q1 — Conceptual

### Execution Flow of try / except / else / finally

**try**
- The code inside the `try` block runs first.
- If an exception occurs, Python stops executing the remaining code in the `try` block and moves to the matching `except` block.

**except**
- Executes only when an exception occurs in the `try` block.
- Used to handle errors and prevent the program from crashing.

**else**
- Runs only if the `try` block completes successfully without any exceptions.

**finally**
- Always executes whether an exception occurs or not.
- Commonly used for cleanup tasks such as closing files or releasing resources.

### Example

```python
try:
    num = int(input("Enter a number: "))
except ValueError:
    print("Invalid input. Please enter a number.")
else:
    print("Double value:", num * 2)
finally:
    print("Program execution finished.")
```

### If an Exception Occurs in the else Block

If an exception happens inside the `else` block, it will **not be caught by the previous `except` block** because `except` only handles errors from the `try` block.  
The exception will propagate upward unless another `try/except` handles it.

---

# Q2 — Coding

## safe_json_load(filepath)

```python
import json
import logging

logging.basicConfig(
    filename="json_errors.log",
    level=logging.ERROR,
    format="%(asctime)s - %(levelname)s - %(message)s"
)

def safe_json_load(filepath):
    try:
        with open(filepath, "r") as f:
            data = json.load(f)
            return data

    except FileNotFoundError as e:
        logging.error(f"File not found: {filepath} | {e}")

    except json.JSONDecodeError as e:
        logging.error(f"Invalid JSON format: {filepath} | {e}")

    except PermissionError as e:
        logging.error(f"Permission denied: {filepath} | {e}")

    return None
```

---

# Q3 — Debug / Analyze

## Corrected Code

```python
def process_data(data_list):
    results = []

    for item in data_list:
        try:
            value = int(item)
            results.append(value * 2)

        except ValueError as e:
            print(f"Error processing item '{item}': {e}")
            continue

    return results
```

## Fixes

1. Replaced the **bare `except`** with `except ValueError` to avoid catching unintended exceptions.

2. Removed the **return inside `finally`**, which previously caused the function to exit during the first loop iteration.

3. Improved the **error message** to show which item caused the failure and why.
