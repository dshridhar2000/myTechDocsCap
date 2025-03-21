# 6.5 Anonymous Functions and Closures

## 1️⃣ Concept Overview

### **What are Anonymous Functions?**
Anonymous functions are **functions without a name**. In Go, you can define them inline, assign them to variables, or use them as arguments in higher-order functions.

### **What are Closures?**
Closures are **functions that capture variables from their surrounding scope**, allowing them to retain and modify state even after the outer function has executed.

### **Why are They Important?**
- **Improves code conciseness** by avoiding unnecessary function declarations.
- **Encapsulates logic** without polluting the global scope.
- **Enables function factories** and **stateful functions**.
- **Used in Goroutines, callbacks, and higher-order functions.**

### **Key Points to Remember**
✔ Anonymous functions can be **immediately invoked** or **assigned to variables**.  
✔ Closures **remember** variables from their enclosing scope.  
✔ Used in **event handling, data filtering, and Goroutines**.

---

## 2️⃣ Syntax & Code Example

### **Basic Syntax of Anonymous Function**
```go
package main

import "fmt"

func main() {
    // Anonymous function assigned to a variable
    add := func(a, b int) int {
        return a + b
    }

    fmt.Println(add(5, 3)) // Output: 8
}
```

### **Immediately Invoked Anonymous Function (IIFE)**
```go
package main

import "fmt"

func main() {
    result := func(a, b int) int {
        return a + b
    }(5, 3) // Calling immediately

    fmt.Println(result) // Output: 8
}
```

---

## 3️⃣ Use Cases with Examples

### **1. Using Closures to Retain State**
Closures are great for keeping state inside a function.

```go
package main

import "fmt"

func counter() func() int {
    count := 0
    return func() int {
        count++
        return count
    }
}

func main() {
    increment := counter() // Create a new counter
    fmt.Println(increment()) // Output: 1
    fmt.Println(increment()) // Output: 2
}
```

### **2. Anonymous Function in Goroutine**
```go
package main

import (
    "fmt"
    "time"
)

func main() {
    go func() {
        fmt.Println("Hello from Goroutine")
    }()
    
    time.Sleep(time.Second) // Wait for Goroutine to complete
}
```

### **3. Using Anonymous Functions as Arguments**
```go
package main

import "fmt"

// Higher-order function that accepts an anonymous function
func applyOperation(a, b int, operation func(int, int) int) int {
    return operation(a, b)
}

func main() {
    sum := applyOperation(5, 3, func(x, y int) int {
        return x + y
    })

    fmt.Println(sum) // Output: 8
}
```

---

## 4️⃣ Best Practices & Common Mistakes

### **✅ Best Practices**
✔ **Use closures for encapsulating logic** when keeping state is necessary.  
✔ **Pass anonymous functions to higher-order functions** for clean, reusable code.  
✔ **Use Goroutines carefully** to avoid race conditions.  

### **❌ Common Mistakes & How to Avoid Them**
🚨 **Modifying a captured variable incorrectly**
```go
package main

import "fmt"

func main() {
    var funcs []func()

    for i := 0; i < 3; i++ {
        funcs = append(funcs, func() {
            fmt.Println(i) // Wrong! Captures final i value (3)
        })
    }

    for _, f := range funcs {
        f() // Prints 3, 3, 3 (unexpected)
    }
}
```
✅ **Fix using function parameters**
```go
func main() {
    var funcs []func()

    for i := 0; i < 3; i++ {
        funcs = append(funcs, func(n int) func() {
            return func() {
                fmt.Println(n) // Captures correct value
            }
        }(i))
    }

    for _, f := range funcs {
        f() // Correctly prints 0, 1, 2
    }
}
```

---

## 5️⃣ Advanced Topics

### **1. Recursive Anonymous Functions**
Go allows anonymous functions to call themselves recursively.

```go
package main

import "fmt"

func main() {
    factorial := func(n int) int {
        if n == 0 {
            return 1
        }
        return n * factorial(n-1)
    }

    fmt.Println(factorial(5)) // Output: 120
}
```

### **2. Closures with Pointers for Performance**
Using **pointers** inside closures can improve performance when dealing with large data structures.

```go
package main

import "fmt"

func main() {
    counter := func() func() *int {
        count := 0
        return func() *int {
            count++
            return &count
        }
    }

    inc := counter()
    fmt.Println(*inc()) // Output: 1
    fmt.Println(*inc()) // Output: 2
}
```

---

## 6️⃣ Interview Questions & Exercises

### **Common Interview Questions**
1. **What is an anonymous function in Go?**
2. **How do closures retain state?**
3. **Can an anonymous function be recursive?**
4. **How do you pass an anonymous function as an argument?**
5. **Explain a real-world use case for closures.**

### **Hands-On Exercises**
✅ **Exercise 1:** Write an anonymous function that calculates the square of a number and immediately executes it.  
✅ **Exercise 2:** Create a closure-based counter that supports increment and decrement operations.  
✅ **Exercise 3:** Implement a higher-order function that takes an array and a function, then applies the function to each element.  

---

## 7️⃣ External References & Documentation

📌 **Official Go Documentation:**  
🔗 [https://go.dev/doc/effective_go#functions](https://go.dev/doc/effective_go#functions)  

📌 **Additional Learning Resources:**  
- [Go by Example - Closures](https://gobyexample.com/closures)  
- [A Deep Dive into Go Anonymous Functions](https://blog.golang.org/first-class-functions-in-go)  
- [Closures in Go: Practical Applications](https://medium.com/swlh/understanding-closures-in-golang-bd50ad51a051)  

---

That’s a **complete guide** to **Anonymous Functions and Closures in Go!** 🚀  
Let me know if you need more examples or explanations! 😊
