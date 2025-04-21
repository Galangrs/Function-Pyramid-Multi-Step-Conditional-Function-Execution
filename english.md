# Function Pyramid (Programming Concept)

## Overview
**Function Pyramid** is a structured approach to organize and execute functions based on certain conditions. This concept is designed to solve complex logical problems, where multiple functions need to be executed in a specific order depending on predefined values or results. These functions are executed **sequentially**, and each function can modify the status or value used by the next function.

**Function Pyramid** helps manage execution flows in scenarios like validation, search algorithms, or complex decision-making processes, where functions need to work together in a structured order without conflicts.

---

## Key Benefits
- **Tiered Execution**: Functions can be nested or structured, allowing them to safely store and manipulate state.
- **Condition-Based Logic**: This system allows execution based on certain conditions (e.g., values or results) in a structured manner.
- **Global Application**: These functions can be used globally within a system, ensuring there are no logic errors or conflicts during execution.
- **Reusability**: The same functions can be reused without duplication as long as the conditions are met.

---

## Primary Use Cases
- **Function Execution Based on Condition**: Functions are executed based on a specific return value or result.
- **Status Management**: Functions can maintain and update the status between executions.
- **Sequential Execution**: Functions are executed step by step, ensuring that each step only happens if the previous one meets the required conditions.

---

## Basic Structure of Function Pyramid

### Pseudocode Logic:
The following pseudocode describes the basic operation of the **Function Pyramid** logic.

1. Define a list of functions.
2. Each function should include:
   - A condition (return value or result).
   - A function that performs a specific operation (e.g., computation, validation).
3. Define a target value or result.
4. Execute each function:
   - Check if the function’s condition matches the target value.
   - If it matches, execute that function.
   - Continue until all functions are evaluated.

```plaintext
FOR each function in the list of functions:
    IF function's return value matches the target value:
        EXECUTE the function
```

---

## Example Implementations

### 1. JavaScript Example
```javascript
const pyramid = [
    {
        func: async () => {
            console.log("Execute function with return 2");
        },
        return: 2
    },
    {
        func: async () => {
            console.log("Execute function with return 1");
        },
        return: 1
    }
];

const targetValue = 2;

(async () => {
    for (let i = 0; i < pyramid.length; i++) {
        if (pyramid[i].return === targetValue) {
            await pyramid[i].func();
        }
    }
})();
```

### 2. Lua Example
```lua
local pyramid = {
    {
        func = function()
            print("Execute function with return 2")
        end,
        result = 2
    },
    {
        func = function()
            print("Execute function with return 1")
        end,
        result = 1
    },
}

local target_value = 2

for i = 1, #pyramid do
    if pyramid[i].result == target_value then
        pyramid[i].func()
    end
end
```

### ✅ Python Example
```python
pyramid = [
    {
        "func": lambda: print("Execute function with return 2"),
        "result": 2
    },
    {
        "func": lambda: print("Execute function with return 1"),
        "result": 1
    }
]

desired_value = 2

for item in pyramid:
    if item["result"] == desired_value:
        item["func"]()
```

---

## Advanced Example

In more advanced cases, functions can modify their results and execute recursively, updating their status until the target value is reached.

### JavaScript
```javascript
const pyramid = [
    {
        result: 1,
        async func(maxValue) {
            console.log(`Execute function 1, result = ${this.result}`);
            if (this.result < maxValue) {
                this.result += 1;
                await this.func(maxValue);
            }
        }
    },
    {
        result: 10,
        async func(maxValue) {
            console.log(`Execute function 2, result = ${this.result}`);
            if (this.result < maxValue) {
                this.result += 1;
                await this.func(maxValue);
            }
        }
    },
    {
        result: 3,
        async func(maxValue) {
            console.log(`Execute function 3, result = ${this.result}`);
            if (this.result < maxValue) {
                this.result += 1;
                await this.func(maxValue);
            }
        }
    }
];

const maxValue = 10;

(async function main() {
    for (let i = 0; i < pyramid.length; i++) {
        if (pyramid[i].result < maxValue) {
            await pyramid[i].func.call(pyramid[i], maxValue);
        }
    }

    console.log(
        `\nFinal results:\nFunction 1: ${pyramid[0].result}, Function 2: ${pyramid[1].result}, Function 3: ${pyramid[2].result}`
    );
})();
```

### Lua
```lua
local pyramid = {
    [1] = {
        func = function(self, max_value)
            print("Execute function 1, result =", self.result)
            if self.result < max_value then
                self.result = self.result + 1
                self:func(max_value)
            end
        end,
        result = 1
    },
    [2] = {
        func = function(self, max_value)
            print("Execute function 2, result =", self.result)
            if self.result < max_value then
                self.result = self.result + 1
                self:func(max_value)
            end
        end,
        result = 10
    },
    [3] = {
        func = function(self, max_value)
            print("Execute function 3, result =", self.result)
            if self.result < max_value then
                self.result = self.result + 1
                self:func(max_value)
            end
        end,
        result = 3
    },
}

local max_value = 10

function main()
    for i = 1, #pyramid do
        if pyramid[i].result < max_value then
            pyramid[i]:func(max_value)
        end
    end
end

main()

print(pyramid[1].result, pyramid[2].result, pyramid[3].result)
```

### Python
```python
class PyramidFunction:
    def __init__(self, result):
        self.result = result

    def func(self, max_value):
        print(f"Execute function, result = {self.result}")
        if self.result < max_value:
            self.result += 1
            self.func(max_value)

pyramid = [
    PyramidFunction(1),
    PyramidFunction(10),
    PyramidFunction(3)
]

max_value = 10

def main():
    for pf in pyramid:
        if pf.result < max_value:
            pf.func(max_value)

main()

print("\nFinal results:")
for i, pf in enumerate(pyramid):
    print(f"Function {i+1}: {pf.result}")
```

---

## Middleware Pipeline & Multi-Step Validation

### Middleware Pipeline Pattern
In addition to **Function Pyramid**, the **middleware pipeline pattern** can be used, where each step in the process acts as middleware. Each function modifies the context and passes it to the next step.

### Pseudocode for Middleware Pipeline:
1. Create a list of middleware functions.
2. Each middleware modifies the context and passes it to the next function.
3. Execute all middleware functions sequentially.

```plaintext
FOR each middleware in the list of middleware:
    MODIFY context
    PASS context to the next middleware
```

---

## Function Pyramid vs. Regular Functions

### Function Pyramid:
1. **Sequential Execution Based on Condition**: Functions in the pyramid are executed in a specific order, each depending on certain conditions (e.g., matching values). They can call each other and update their statuses in a nested manner.
2. **Status Management**: Each function can retain its status and update it, allowing for more dynamic and flexible execution.
3. **Recursive Capability**: Functions can recursively call themselves to continue execution until the desired condition is met.
4. **Global Application**: The system ensures that all functions in the pyramid work together without conflicts or errors.

### Regular Functions:
1. **Independent Execution**: Functions are typically executed independently, with no guaranteed order unless explicitly defined.
2. **No Built-in Status Management**: Regular functions don’t typically retain or pass along status unless explicitly shared via variables or objects.
3. **No Automatic Recursive or Condition-Based Execution**: Functions do not automatically adjust their execution flow based on conditions or recursive calls unless programmed to do so.
4. **Limited Context**: Regular functions may not always have access to other functions' statuses or contexts unless explicitly passed.

---

## Conclusion
**Function Pyramid** is a powerful concept for managing the sequential execution of functions in complex scenarios. It can be used for conditional processing, multi-step validation, and middleware pipelines. By combining this approach, developers can handle multi-stage workflows while maintaining clean and manageable code.

This documentation provides a clear understanding of **Function Pyramid** and compares it with regular functions to highlight its advantages in managing complex logic flows.
