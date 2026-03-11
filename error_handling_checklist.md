Here is a **clean copy-paste Markdown version** you can directly put into your `.md` file.

````markdown
# Part A — Error Handling Refactor

## Overview
In this task, three programs from earlier exercises were improved by adding proper exception handling, input validation, and logging. The goal is to make the programs safer when handling user input or unexpected errors.

---

# Program 1 — Age Calculator

## Code

```python
while True:
    try:
        age = int(input("Enter your age: "))

        if age < 0 or age > 150:
            raise ValueError("Age must be between 0 and 150")

    except ValueError as e:
        print(f"Invalid input: {e}. Please try again.")

    else:
        print(f"In 10 years you will be {age + 10}")
        break

    finally:
        print("Input attempt completed.\n")
````

---

# Program 2 — Division Program

## Code

```python
while True:
    try:
        num1 = float(input("Enter first number: "))
        num2 = float(input("Enter second number: "))

        if num2 == 0:
            raise ZeroDivisionError("Second number cannot be zero")

    except ValueError:
        print("Please enter valid numeric values.")

    except ZeroDivisionError as e:
        print(e)

    else:
        result = num1 / num2
        print("Result:", result)
        break

    finally:
        print("Division attempt finished.\n")
```

---

# Program 3 — Product Lookup with Logging

## Code

```python
import logging

logging.basicConfig(
    filename="error_log.txt",
    level=logging.ERROR,
    format="%(asctime)s - %(levelname)s - %(message)s"
)

products = {
    "laptop": 75000,
    "mouse": 800,
    "keyboard": 2500
}

while True:
    try:
        item = input("Enter product name: ").lower()

        if item not in products:
            raise KeyError("Product not found")

    except KeyError as e:
        print("Sorry, that product does not exist.")
        logging.error(f"Invalid product lookup: {item}")

    else:
        print(f"Price of {item} is {products[item]}")
        break

    finally:
        print("Lookup attempt completed.\n")
```

---

# error_handling_checklist.md

## Program 1 — Age Calculator

**Exceptions Caught**

* ValueError

**Recovery Action**

* Ask the user to enter the age again.

**User Sees**

* "Invalid input. Please try again."

**Logged Internally**

* No logging used.

---

## Program 2 — Division Program

**Exceptions Caught**

* ValueError
* ZeroDivisionError

**Recovery Action**

* User is asked to re-enter numbers.

**User Sees**

* "Please enter valid numeric values."
* "Second number cannot be zero."

**Logged Internally**

* No logging used.

---

## Program 3 — Product Lookup

**Exceptions Caught**

* KeyError

**Recovery Action**

* User is prompted to enter a valid product.

**User Sees**

* "Sorry, that product does not exist."

**Logged Internally**

* Invalid product lookups are recorded in `error_log.txt`.
