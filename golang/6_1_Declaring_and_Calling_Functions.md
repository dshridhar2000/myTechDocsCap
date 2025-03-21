## 6.1 Declaring and Calling Functions 
## 6.2 Function Parameters and Return Values 
## 6.3 Multiple Return Values

### **1️⃣ Brief Description**  
Functions in Go are **self-contained blocks of code** that perform a specific task. They help in **code reusability, modularity, and maintainability**.  

In Go, a function is declared using the `func` keyword, followed by:  
- The function name  
- Parameter list (optional)  
- Return type (optional)  

A function can be called using its name followed by parentheses.  

---

### **2️⃣ Code Example: Declaring and Calling a Function**  

```go
package main

import "fmt"

// Function declaration with parameters and return value
func addNumbers(a int, b int) int {
    sum := a + b  // Perform addition
    return sum    // Return result
}

func main() {
    // Calling the function
    result := addNumbers(10, 20)
    
    // Printing the result
    fmt.Println("Sum:", result)
}
```

### **🔹 Explanation:**
1. The function `addNumbers(a int, b int) int` accepts **two integers** and returns their sum.  
2. The function is called in `main()` with `addNumbers(10, 20)`.  
3. The result is stored in `result` and printed.  

---

### **3️⃣ Use Cases with Examples**  

#### **✅ Use Case 1: Code Reusability**
🔹 **Example**: A function that **calculates the area of a rectangle**.  

```go
package main

import "fmt"

// Function to calculate area
func rectangleArea(length, width float64) float64 {
    return length * width
}

func main() {
    area := rectangleArea(5.5, 4.2)  // Function call
    fmt.Println("Rectangle Area:", area)
}
```
🔹 **Why?**  
Instead of writing the same logic multiple times, we **reuse** the `rectangleArea` function.

---

#### **✅ Use Case 2: Handling Multiple Return Values**
🔹 **Example**: A function that **returns quotient and remainder**.  

```go
package main

import "fmt"

// Function with multiple return values
func divideNumbers(dividend, divisor int) (int, int) {
    quotient := dividend / divisor
    remainder := dividend % divisor
    return quotient, remainder
}

func main() {
    q, r := divideNumbers(10, 3)  // Function call
    fmt.Println("Quotient:", q, "Remainder:", r)
}
```
🔹 **Why?**  
Functions can return **multiple values** at once, making them useful for operations like **division, swapping, and error handling**.

---

#### **✅ Use Case 3: Anonymous Functions (Useful for Short Operations)**
🔹 **Example**: A quick function to **calculate the square of a number**.  

```go
package main

import "fmt"

func main() {
    square := func(n int) int {  // Anonymous function
        return n * n
    }

    fmt.Println("Square of 6:", square(6))
}
```
🔹 **Why?**  
Anonymous functions **don’t require a name** and are useful for **short, one-time operations**.

---

### **📌 Summary**
- Functions **encapsulate** logic for better reusability and readability.  
- Functions can **accept parameters and return values**.  
- Go supports **multiple return values**.  
- **Anonymous functions** are useful for inline operations.  

Would you like me to cover **recursion or variadic functions** next? 😊
