---
title: Methods For Finding The Factorial Of A Number In JavaScript
date: "2021-05-11T07:26:03.284Z"
description: "Post displaying the various ways of finding the factorial of a number in JavaScript"
categories: [code]
comments: true
---

In Mathematics, the **factorial** of a non-negative​ integer n, denoted by n!, is computed as the product of all positive integers less than or equal to n [^1]:

[^1]: https://en.wikipedia.org/wiki/Factorial

`n! = n*(n-1)*(n-2)*(n-3)...3*2*1`

When you factorialize an integer, you are multiplying that integer by each consecutive integer minus one.

If the integer is 6, the factorial would be:

`6! = 6 * 5 * 4 * 3 * 2 * 1`

The pattern would be:

```javascript
0! = 1
1! = 1
2! = 2 * 1
3! = 3 * 2 * 1
4! = 4 * 3 * 2 * 1
5! = 5 * 4 * 3 * 2 * 1
6! = 6 * 5 * 4 * 3 * 2 * 1
```

# Methods

There are two methods we can use to find the factorial of a number in JavaScript.

- Iteration
- Recursion

## 1. The Iterative Method

In computer programming, `iteration` is a sequence of instructions that is continually repeated. You can think of iteration as a loop [^1].

[^1]: https://computersciencewiki.org/index.php/Iteration#:~:text=In%20computer%20programming%2C%20iteration%20is,iteration%22%20or%20%22iterate%22.&text=iterate%20until%20a%20certain%20condition,in%20a%20list%20or%20array

We will use two types of iterations (loops):

- WHILE loop (iterate until a certain condition is reached)
- FOR loop (iterate a certain number of times)

### a. Using **WHILE** loop

```javascript
const factorialize = num => {
  // Step 1. Create a variable factorial to store num
  let factorial = num

  //If a negative num is entered, reject
  if (num < 0) {
    return -1
  }

  // If num = 0 OR num = 1, the factorial will return 1
  if (num === 0 || num === 1) {
    return 1
  }

  // Step 2. Create the WHILE loop
  while (num > 1) {
    num-- // decrement by 1 at each iteration
    factorial = factorial * num // or factorial *= num;

    /* 
                    num           num--      let factorial      factorial *= num         
    1st iteration:   6             5            6             30 = 6 * 5      
    2nd iteration:   5             4           30             120 = 30 * 4
    3rd iteration:   4             3           120            360 = 120 * 3
    4th iteration:   3             2           360            720 = 360 * 2
    5th iteration:   2             1           720            720 = 720 * 1
    6th iteration    1             0           720
    End of the WHILE loop 
    */

    // Step 3. Return the factorial of the provided integer
    return factorial // 720
  }

  factorialize(6)
}
```

### b. Using **FOR** loop

```javascript
const factorialize = num => {
  // If num = 0 OR num = 1, the factorial will return 1
  if (num === 0 || num === 1) {
    return 1
  }

  // We start the FOR loop with i = 4
  // We decrement i after each iteration
  for (let i = num - 1; i >= 1; i--) {
    // We store the value of num at each iteration
    num = num * i // or num *= i;
    /* 
                    num      let i = num - 1       num *= i         i--       i >= 1?
    1st iteration:   5           4 = 5 - 1         20 = 5 * 4        3          yes   
    2nd iteration:  20           3 = 4 - 1         60 = 20 * 3       2          yes
    3rd iteration:  60           2 = 3 - 1        120 = 60 * 2       1          yes  
    4th iteration: 120           1 = 2 - 1        120 = 120 * 1      0          no             
    5th iteration: 120               0                120
    End of the FOR loop 
    */
  }
  return num //120
}

factorialize(5)
```

**Pro**: Iteration Takes less memory than the recursive implementation.
**Con**: The code is lengthier than that of the recursive implementation.

## 2. The Recursive Method

In computer science, `recursion` is a method of solving a problem where the solution depends on solutions to smaller instances of the same problem [^1]. It is implemented by allowing a function to call itself from within its own code.

[^1]: https://en.wikipedia.org/wiki/Recursion_(computer_science)#:~:text=In%20computer%20science%2C%20recursion%20is,instances%20of%20the%20same%20problem.&text=Most%20computer%20programming%20languages%20support,from%20within%20its%20own%20code.

Enough talk. Let's code!

```javascript
const factorialize = num => {
  // If the number is less than 0, reject it.
  if (num < 0) {
    return -1
  }

  // If the number is 0, its factorial is 1.
  else if (num == 0) {
    return 1
  }

  // Otherwise, call the recursive procedure again
  else {
    return num * factorialize(num - 1)
    /* 
        First Part of the recursion method
        You need to remember that you won’t have just one call, you’ll have several nested calls
        
        Each call: num === "?"        	         num * factorialize(num - 1)
        1st call – factorialize(5) will return    5  * factorialize(5 - 1) // factorialize(4)
        2nd call – factorialize(4) will return    4  * factorialize(4 - 1) // factorialize(3)
        3rd call – factorialize(3) will return    3  * factorialize(3 - 1) // factorialize(2)
        4th call – factorialize(2) will return    2  * factorialize(2 - 1) // factorialize(1)
        5th call – factorialize(1) will return    1  * factorialize(1 - 1) // factorialize(0)
        
        Second part of the recursion method
        The method hits the if condition, it returns 1 which num will multiply itself with
        The function will exit with the total value
        
        5th call will return (5 * (5 - 1))     // num = 5 * 4
        4th call will return (20 * (4 - 1))    // num = 20 * 3
        3rd call will return (60 * (3 - 1))    // num = 60 * 2
        2nd call will return (120 * (2 - 1))   // num = 120 * 1
        1st call will return (120)             // num = 120
        
        If we sum up all the calls in one line, we have
        (5 * (5 - 1) * (4 - 1) * (3 - 1) * (2 - 1)) = 5 * 4 * 3 * 2 * 1 = 120
        */
  }
}
factorialize(5)
```

### **Without comments**

```javascript
const factorialize = num => {
  if (num < 0) return -1
  else if (num == 0) return 1
  else {
    return num * factorialize(num - 1)
  }
}
factorialize(5)
```

**Pro**: Recursion has a shorter and cleaner code.
**Con**: Greater memory requirements as all the function calls remain on the stack until the base case is reached.

I hope this helps. Watch out for more tutorials!
