# 🐍 Python Execution, REPL, Bytecode & Development Environments

This document covers Python fundamentals through a review quiz, execution environments, the REPL architecture, script execution, bytecode generation, and Visual Studio Code setup.

---

# 📚 Core Python Concepts Review Quiz

## Q1. What is the correct print syntax in Python 2?

### Answer

```python
print "Hello"
```

### Explanation

In Python 2, `print` was a statement and did not require parentheses.

---

## Q2. What is the correct print syntax in Python 3?

### Answer

```python
print("Hello")
```

### Explanation

In Python 3, `print()` became a built-in function, making parentheses mandatory.

---

## Q3. Is Python case-sensitive?

### Answer

✅ Yes

### Example

```python
print("Hello")   # Correct
Print("Hello")   # NameError
PRINT("Hello")   # NameError
```

---

## Q4. Is Python interpreted or compiled?

### Answer

✅ Both

### Explanation

Python first compiles source code into Bytecode and then executes it through the Python Virtual Machine (PVM).

---

## Q5. Are Python programs generally shorter than equivalent C or Java programs?

### Answer

✅ True

Python allows developers to accomplish tasks using significantly fewer lines of code.

---

## Q6. Does Python execute faster than C?

### Answer

❌ False

C programs generally execute faster because they compile directly into machine code.

---

## Q7. What does the Python compiler generate?

### Answer

**Bytecode (.pyc)**

---

## Q8. What is CPython?

### Answer

CPython is the official reference implementation of Python written in **C** and maintained by the **Python Software Foundation (PSF)**.

---

## Q9. What converts Bytecode into machine instructions?

### Answer

**Python Virtual Machine (PVM)**

---

## Q10. Is Python 3 backward compatible with Python 2?

### Answer

❌ No

Python 2 code often requires modification before running in Python 3.

---

## Q11. When did Python 2 reach End of Life?

### Answer

📅 January 1, 2020

### Note

Python 2 is still available for download from the official archives, but it no longer receives support, updates, or security patches.

---

## Q12. Rank these by execution speed.

### Answer

```text
C → PyPy → CPython
```

---

## Q13. Which implementation uses JIT Compilation?

### Answer

**PyPy**

### Note

PyPy uses a Just-In-Time (JIT) Compiler and can be approximately **3× faster than CPython** for many workloads.

---

## Q14. What is the output of:

```python
10 / 4
```

### Answer

```python
2.5
```

Python 3 performs true division.

---

## Q15. What happens if you write:

```python
print "Python RX"
```

in Python 3?

### Answer

❌ SyntaxError

Because parentheses are required.

---

## Q16. Is machine code platform independent?

### Answer

❌ No

Machine code is platform dependent and specific to CPU architectures.

---

## Q17. What is the extension of Python Bytecode files?

### Answer

```text
.pyc
```

---

## Q18. Is Python statically typed?

### Answer

❌ No

Python is dynamically typed.

Example:

```python
x = 10
x = "Hello"
```

The variable can hold different data types during runtime.

---

# 🚀 Six Ways to Run Python Code

Python programs can be executed using several environments.

## 1. Interactive Mode (Python Shell)

Execute commands directly from the terminal.

```bash
python
```

---

## 2. Script Mode

Execute saved Python files.

```bash
python program.py
```

---

## 3. IDLE

Integrated Development and Learning Environment provided by Python.

---

## 4. Jupyter Notebook

Popular environment for:

* Data Science
* Machine Learning
* AI Development

---

## 5. IDEs

Examples:

* VS Code
* PyCharm

---

## 6. Cloud Platforms

Examples:

* Google Colab
* Kaggle Notebooks

---

# 🔄 Interactive Mode & REPL Architecture

Interactive mode allows instant execution of Python commands.

When launched, the Python shell displays:

```python
>>>
```

---

## REPL Model

Python Interactive Mode follows the REPL architecture.

### R — Read

Reads user input.

### E — Evaluate

Processes the expression.

### P — Print

Displays the result.

### L — Loop

Waits for the next command.

---

### REPL Flow

```text
Read
  ↓
Evaluate
  ↓
Print
  ↓
Loop
  ↺
```

---

# 📖 Help System & Keywords

Python provides a built-in help utility.

```python
help()
```

Inside help mode:

```python
help> keywords
```

This displays all Python reserved keywords.

---

## Important Fact

Python 3.13 contains **35 reserved keywords**.

Only three begin with uppercase letters:

```python
True
False
None
```

Python keywords are case-sensitive.

---

# 📄 Script Mode

Script mode involves writing Python code in a `.py` file and executing it.

Example:

```python
print("Hello Python")
```

Save as:

```text
first_code.py
```

Run using:

```bash
python first_code.py
```

---

# ⚙️ Manual Bytecode Generation

Normally CPython creates Bytecode automatically.

To manually generate Bytecode:

```bash
python -m py_compile first_code.py
```

---

## Understanding the Command

### -m

Module execution switch.

### py_compile

Python's built-in compilation module.

---

# 📁 Dunder PyCache

After compilation, Python creates:

```text
__pycache__
```

This is pronounced:

> Dunder PyCache

("Dunder" means double underscore.)

Inside it you'll find:

```text
first_code.cpython-313.pyc
```

---

# 🔍 Python Execution Pipeline

```text
Source Code (.py)
        │
        ▼
   Python Compiler
        │
        ▼
  Bytecode (.pyc)
        │
        ▼
Python Virtual Machine
        │
        ▼
   Machine Code
        │
        ▼
       CPU
```

---

# 💻 Visual Studio Code Setup

## Step 1: Install VS Code

Download and install Visual Studio Code for your operating system.

---

## Step 2: Install Python Extension

1. Open VS Code
2. Click Extensions
3. Search:

```text
Python
```

4. Install the official Microsoft extension.

---

## Step 3: Optional Enhancements

Install:

```text
Material Icon Theme
```

for better workspace visuals.

---

## Step 4: Open Project Folder

Navigate to:

```text
File → Open Folder
```

and select your project directory.

---

## Step 5: Create Python Files

Example:

```text
test.py
```

---

## Step 6: Run Programs

### Method 1

Use the ▶ Run button.

### Method 2

Use the integrated terminal:

```bash
python test.py
```

---

# 🎯 Key Takeaways

* Python is both compiled and interpreted.
* Source code is first converted into Bytecode.
* The Python Virtual Machine executes Bytecode.
* Python supports six major execution environments.
* Interactive mode follows the REPL model.
* Python keywords are case-sensitive.
* Bytecode files use the `.pyc` extension.
* The `__pycache__` directory stores compiled Bytecode.
* VS Code is one of the most popular IDEs for Python development.
* PyPy uses JIT Compilation and can be approximately 3× faster than CPython.
