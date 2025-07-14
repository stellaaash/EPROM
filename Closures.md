---
tags:
  - programming_concept
---
Closures are when a function returns another function that **"remembers" variables local to the outer function**.
The inner function will retain access to the members of the outer function **even after that one has finished execution and returned the inner function.**
Many widespread languages have closures as a feature, such as Python, Ruby and JavaScript.
___
**Here's a pretty well done metaphor by my good friend Claude:**
> Here's a mental exercise that might help solidify this: imagine you're a function in JavaScript, and you're about to be shipped off to be executed somewhere else. As you're leaving your home environment, you can grab any variables you can see and stuff them in your backpack to take with you. That's closure.
# Examples
```js
function createCounter() {
    let count = 0; // This variable lives in createCounter's scope
    
    return function() {
        count++; // The inner function can access and modify 'count'
        return count;
    };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```
___
```js
function createBankAccount(initialBalance) {
    let balance = initialBalance;  // This will be captured by closures
    
    return {
        deposit: function(amount) {
            balance += amount;  // Both functions access the same 'balance'
            return balance;
        },
        withdraw: function(amount) {
            if (amount <= balance) {
                balance -= amount;  // Same 'balance' variable
                return balance;
            }
            return "Insufficient funds";
        }
    };
}

const account = createBankAccount(100);
console.log(account.deposit(50));  // 150
console.log(account.withdraw(30)); // 120
```
