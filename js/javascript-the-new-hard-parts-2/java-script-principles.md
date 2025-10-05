# JavaScript Execution Context - Visual Guide

## 📋 Sample Code
```javascript
const num = 3;

function multiplyBy2(inputNumber) {
    const result = inputNumber * 2;
    return result;
}

const output = multiplyBy2(num);
const newOutput = multiplyBy2(10);
```

---

## 🎯 How JavaScript Executes Code

JavaScript runs code **line by line** with two main components:
1. **Thread of Execution** - reads and runs code line by line
2. **Memory** - stores variables and functions

---

## 📊 Step-by-Step Execution with Visuals

### **Step 1: Line 1** - `const num = 3;`

```
╔════════════════════════════════════════╗
║     GLOBAL EXECUTION CONTEXT           ║
╠════════════════════════════════════════╣
║  MEMORY          │  THREAD OF EXECUTION║
║                  │                     ║
║  num: 3          │  → Line 1 ✓        ║
║                  │                     ║
║                  │                     ║
╚════════════════════════════════════════╝
```

---

### **Step 2: Lines 3-6** - Function Definition

```
╔════════════════════════════════════════╗
║     GLOBAL EXECUTION CONTEXT           ║
╠════════════════════════════════════════╣
║  MEMORY          │  THREAD OF EXECUTION║
║                  │                     ║
║  num: 3          │  → Lines 3-6 ✓     ║
║                  │                     ║
║  multiplyBy2: f{}│                     ║
║  (function code) │                     ║
║                  │                     ║
╚════════════════════════════════════════╝
```

**Note:** `multiplyBy2` stores the entire function as an object

---

### **Step 3: Line 8** - `const output = multiplyBy2(num);`

#### 3a. Function Call Initiated
```
╔════════════════════════════════════════╗
║     GLOBAL EXECUTION CONTEXT           ║
╠════════════════════════════════════════╣
║  MEMORY          │  THREAD OF EXECUTION║
║                  │                     ║
║  num: 3          │  → Line 8          ║
║  multiplyBy2: f{}│  (PAUSED)          ║
║  output: ???     │  Calling function...║
║                  │                     ║
╚════════════════════════════════════════╝
                    ↓
        Creating Local Execution Context
```

#### 3b. Local Execution Context Created
```
        ╔════════════════════════════════════════╗
        ║  LOCAL EXECUTION CONTEXT               ║
        ║  multiplyBy2(3)                        ║
        ╠════════════════════════════════════════╣
        ║  MEMORY          │  THREAD OF EXECUTION║
        ║                  │                     ║
        ║  inputNumber: 3  │  → Line 4          ║
        ║  (parameter)     │                     ║
        ║                  │                     ║
        ║  result: ???     │                     ║
        ║                  │                     ║
        ╚════════════════════════════════════════╝

╔════════════════════════════════════════╗
║     GLOBAL EXECUTION CONTEXT           ║
║                (PAUSED)                 ║
╠════════════════════════════════════════╣
║  num: 3                                ║
║  multiplyBy2: f{}                      ║
║  output: ???                           ║
╚════════════════════════════════════════╝
```

#### 3c. Calculate Result
```
        ╔════════════════════════════════════════╗
        ║  LOCAL EXECUTION CONTEXT               ║
        ║  multiplyBy2(3)                        ║
        ╠════════════════════════════════════════╣
        ║  MEMORY          │  THREAD OF EXECUTION║
        ║                  │                     ║
        ║  inputNumber: 3  │  → Line 4 ✓        ║
        ║                  │  3 * 2 = 6         ║
        ║  result: 6       │                     ║
        ║                  │                     ║
        ╚════════════════════════════════════════╝
```

#### 3d. Return Value
```
        ╔════════════════════════════════════════╗
        ║  LOCAL EXECUTION CONTEXT               ║
        ║  multiplyBy2(3)                        ║
        ╠════════════════════════════════════════╣
        ║  MEMORY          │  THREAD OF EXECUTION║
        ║                  │                     ║
        ║  inputNumber: 3  │  → Line 5 ✓        ║
        ║  result: 6       │  return 6          ║
        ║                  │                     ║
        ╚════════════════════════════════════════╝
                    ↓
            Returning value 6
                    ↓
╔════════════════════════════════════════╗
║     GLOBAL EXECUTION CONTEXT           ║
║              (RESUMED)                  ║
╠════════════════════════════════════════╣
║  num: 3                                ║
║  multiplyBy2: f{}                      ║
║  output: 6  ← (value returned)         ║
╚════════════════════════════════════════╝
```

**Local Execution Context is DELETED after return**

---

### **Step 4: Line 9** - `const newOutput = multiplyBy2(10);`

Same process repeats:

```
        ╔════════════════════════════════════════╗
        ║  LOCAL EXECUTION CONTEXT               ║
        ║  multiplyBy2(10)                       ║
        ╠════════════════════════════════════════╣
        ║  inputNumber: 10                       ║
        ║  result: 20                            ║
        ║                                        ║
        ║  returns → 20                          ║
        ╚════════════════════════════════════════╝
                    ↓
╔════════════════════════════════════════╗
║     GLOBAL EXECUTION CONTEXT           ║
╠════════════════════════════════════════╣
║  num: 3                                ║
║  multiplyBy2: f{}                      ║
║  output: 6                             ║
║  newOutput: 20  ← (value returned)     ║
╚════════════════════════════════════════╝
```

---

## 🔄 Call Stack Visualization

The **Call Stack** tracks which execution context is running.

### Initial State
```
┌─────────────────────┐
│                     │
│                     │
│                     │
├─────────────────────┤
│  Global Context     │ ← START HERE
└─────────────────────┘
```

### When `multiplyBy2(num)` is called
```
┌─────────────────────┐
│  multiplyBy2(3)     │ ← CURRENTLY EXECUTING
├─────────────────────┤
│  Global Context     │ ← PAUSED
└─────────────────────┘
```

### After `return` statement
```
┌─────────────────────┐
│                     │ ← multiplyBy2 REMOVED
│                     │
│                     │
├─────────────────────┤
│  Global Context     │ ← BACK TO EXECUTING
└─────────────────────┘
```

### When `multiplyBy2(10)` is called
```
┌─────────────────────┐
│  multiplyBy2(10)    │ ← NEW CALL
├─────────────────────┤
│  Global Context     │ ← PAUSED AGAIN
└─────────────────────┘
```

### After second `return`
```
┌─────────────────────┐
│                     │
│                     │
│                     │
├─────────────────────┤
│  Global Context     │ ← FINISHED
└─────────────────────┘
```

---

## 📚 Key Terms Reference

| Term | Definition | Example |
|------|------------|---------|
| **Identifier** | Variable or function name | `num`, `multiplyBy2` |
| **Execution Context** | Memory + Thread of Execution | Global or Local |
| **Parameter** | Variable in function definition | `inputNumber` |
| **Argument** | Actual value passed to function | `3` or `10` |
| **Call Stack** | Tracks which context is running | Stack structure |
| **Thread of Execution** | Runs code line by line | Like a cursor moving through code |
| **Global Context** | Main execution environment | Always at bottom of call stack |
| **Local Context** | Created when function runs | Temporary, deleted after return |

---

## 🎓 Important Concepts

### 1. **Single-Threaded Execution**
JavaScript can only do **ONE thing at a time**.

```
Global → PAUSE → Local → Execute → Return → RESUME Global
```

### 2. **Context Switching**
```
Running Global Code
        ↓
Function Called → PAUSE Global
        ↓
Create Local Context
        ↓
Run Function Code
        ↓
Return Value → DELETE Local
        ↓
RESUME Global Code
```

### 3. **Memory Management**
- **Global Memory:** Exists throughout program
- **Local Memory:** Created and destroyed with function calls

---

## ✅ Summary

1. JavaScript executes code **line by line**
2. Every execution needs **Memory** + **Thread of Execution** = **Execution Context**
3. **Global Context** is the default starting point
4. **Local Context** is created for each function call
5. **Call Stack** manages which context is currently running
6. JavaScript is **single-threaded** - only one task at a time
7. When a function returns, its local context is **deleted**

---

## 🔍 Common Beginner Mistakes

❌ **Wrong:** Thinking JavaScript can run multiple functions simultaneously
✅ **Right:** JavaScript runs one function at a time (single-threaded)

❌ **Wrong:** Local variables are accessible outside the function
✅ **Right:** Local variables are deleted when function returns

❌ **Wrong:** The call stack is unlimited
✅ **Right:** Too many function calls cause "Stack Overflow" error