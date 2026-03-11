# Part D — AI-Augmented Task

## 1. Prompt Used

```
Write a Python decorator called @retry(max_attempts=3, delay=1) that automatically retries a function if it raises an exception. 
The retry mechanism should use exponential backoff between attempts. 
The decorator should retry the function up to the specified number of attempts and wait longer after each failure.
```

---

# 2. AI Generated Code

```python
import time
import functools

def retry(max_attempts=3, delay=1):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            attempts = 0
            wait = delay

            while attempts < max_attempts:
                try:
                    return func(*args, **kwargs)

                except Exception as e:
                    attempts += 1

                    if attempts >= max_attempts:
                        raise

                    print(f"Attempt {attempts} failed: {e}. Retrying in {wait} seconds...")
                    time.sleep(wait)

                    wait *= 2

        return wrapper
    return decorator
```

---

# 3. Testing the Decorator

```python
import random

@retry(max_attempts=3, delay=1)
def unstable_function():
    if random.random() < 0.5:
        raise ValueError("Random failure occurred")
    return "Success"

for _ in range(5):
    try:
        print(unstable_function())
    except Exception as e:
        print("Final failure:", e)
```

The test function fails randomly about 50% of the time.  
The decorator retries the function automatically with exponential backoff.

---

# 4. Critical Evaluation (Approx. 200 Words)

The AI-generated solution correctly implements a retry decorator that retries a function when an exception occurs. The decorator uses exponential backoff by doubling the delay time after each failed attempt, which is a common technique used in production systems to avoid overwhelming resources during repeated failures. Another positive aspect of the implementation is the use of `functools.wraps`, which preserves the original function’s metadata such as its name and documentation. This is important when decorators are used in larger applications or frameworks.

However, the solution has some limitations. The decorator retries on every type of exception because it catches the generic `Exception` class. In real systems, it is often better to retry only specific exceptions such as network errors or temporary resource issues. Retrying on all exceptions could hide serious programming errors that should not be retried. Another limitation is that the code prints messages directly to the console instead of using a logging system.

Additionally, the implementation does not allow customization of retryable exception types. A more robust design would allow the user to specify which exceptions should trigger a retry. Improvements could include adding logging support, allowing configurable exception types, and adding jitter to the delay to reduce the chance of synchronized retries in distributed systems.
