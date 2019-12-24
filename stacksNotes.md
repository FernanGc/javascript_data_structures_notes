

# Stacks Notes | Data Structures

#### Creating an array-based Stack class

````javascript
class Stack {
    constructor() {
        this.count = 0; // To keep track the size of the stack
        this.items = {};
    }
}
````

> The array data structure allows to add or remove elements from any position in the data structure, but we limit the functionalities to follow the LIFO principle.

#### Pushing elements to the stack

````javascript
push(element) {
 this.items[this.count] = element;
 this.count++;
}
````

> This method adds a new element (or several elements) to the top of the stack.

#### Popping elements from the stack

`````javascript
pop() {
  if (this.isEmpty()) {
      return undefined;
  }

  this.count--;
  const result = this.items[this.count];
  delete this.items[this.count];
  return result;
}
`````

> This method is responsible for removing the items from the stack

#### Peeking the element from the top of the stack

````javascript
peek() {
  if (this.isEmpty()) {
      return undefined;
  }
  return this.items[this.count - 1];
}
````

> This method will return the item from the top of the stack

#### Verifying whether the stack is empty

````javascript
isEmpty() {
  return this.count === 0;
}
````

> This method returns `true` if the stack is empty and `false` otherwise

#### Verifying  the stack size

````javascript
size() {
  return this.count;
}
````

> We simply return the count property

#### Clearing the elements of the stack

````javascript
clear() {
  this.items = {};
  this.count = 0;
}
````

> The `clear` method simply empties the stack removing all its elements.

## A JavaScript object-based Stack class

````javascript
export default class Stack {
    constructor() {
        this.count = 0; // To keep track of the size of the stack
        this.items = {};
    }

    // Pushing elements to the stack
    push(element) {
        this.items[this.count] = element;
        this.count++;
    }

    // Verifying whether the stack is empty and its size
    // For the size method, we can simply return the count property
    size() {
        return this.count;
    }

    // Verify whether the stack is empty, we can compare if the count value is 0 as follows
    isEmpty() {
        return this.count === 0;
    }

    // Popping elements from the stack
    /**
     * {1} Verify whether the stack is empty, if so, we return the value undefined
     * {2} If the stack is not empty, we will decrement the count property
     * {3} Store the value from the top of the stack so we can return it
     * {4} remove the element at the top
     * {5} return the element
     */
    pop() {
        if (this.isEmpty()) { /// {1}
            return undefined;
        }
      
        this.count--; // {2}
        const result = this.items[this.count]; // {3}
        delete this.items[this.count]; // {4}
        return result; // {5}
    }

    // Peeking the top of the stack and clearing it
    peek() {
        if (this.isEmpty()) {
            return undefined;
        }
        return this.items[this.count - 1];
    }

    // Crear the stack, we can simply reset it to the same values we used in the constructor
    clear() {
        this.items = {};
        this.count = 0;
    }

    /**
     * {1} if the stack is not empty we initialize the string with the first element
     * {2} Iterate through all the keys of the stack until its top
     */
    toString() {
        if (this.isEmpty) {
            return '';
        }

        let objString = `${this.items[0]}`; // {1}
        for (let i = 1; i < this.count; i++) { // {2}
            objString = `${objString}, ${this.items[i]}`; // {3}
        }

        return objString;
    }
}
````

#### Using the object-based Stack class

````javascript
const stack = new Stack();
console.log(stack.isEmpty()); // outputs true

// Add some elements
stack.push(5);
stack.push(8);

// Call the peek method
console.log(stack.peek()); // outputs 8
````

# Solving problems using stacks

### Decimal to Binary

> To convent a decimal number into a binary representation, we can divide the number by 2 (binary is a base 2 number system) until the divison result is 0. As example we will convert the number 10 into binary digits:

````pseudocode
10/2 == 5 rem == 0
5/2  == 2 rem == 1
2/2  == 1 rem == 0
1/2  == 0 rem == 1

push iteration ===>
[0] [1] [0] [1]
<=== output = pop remainders
[1] [0] [1] [0]	
````


> **{1}** While the division result is not zero, we get the remainder of the division.
>
> **{2}, {3}** Push the remainder to the stack
>
> **{4}** We update the number that will be divided by 2
>
> {**5}** We pop the elements from the stack until it is empty, concatenating the elements that were removed from the stack into a string.


```javascript
import Stack from './modules/stack.js';

function decimalToBinary(decNumber) {
    const remStack = new Stack();
    let number = decNumber;
    let rem;
    let binaryString = '';

    while (number > 0) { // {1}
        rem = Math.floor(number % 2); // {2}
        remStack.push(rem); // {3}
        number = Math.floor(number / 2); // {4}
    }

    while (!remStack.isEmpty()) { // {5}
        binaryString += remStack.pop().toString();
    }

    return binaryString;
}
```

#### Using the dicimalToBinary function

````javascript
 console.log(decimalToBinary(233));
 console.log(decimalToBinary(10));
 console.log(decimalToBinary(1000));
````

### The base converter algorithm

> Convert from decimal to the bases between 2 and 36. In the conversion from  decimal to binary, the remainders will be 0 or 1; in the conversion from decimal to octagonal, the remainders will be from 0 to 8; and in the  conversion from decimal to hexadecimal, the remainders can be 0 to 9  plus the letters `A` to `F` (values 10 to 15). For this reason, we need to convert these values as well (lines `{6}` and `{7}`). So, starting at base 11, each letter of the alphabet will represent its base. The letter `A` represents base 11, `B` represents base 12, and so on.

````javascript
function baseConverter(decNumber, base) {
    const remStack = new Stack();
    const digits = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ'; // {6} 
    let number = decNumber;
    let rem;
    let baseString = '';

    if (!(base >= 2 && base <= 36)) {
    	return '';
    }

    while (number > 0) {
        rem = Math.floor(number % base);
        remStack.push(rem);
        number = Math.floor(number / base);
    }

    while (!remStack.isEmpty()) {
    	baseString += digits[remStack.pop()]; // {7}
    } 

    return baseString;
}
````

#### Using the baseConverter function

````javascript
console.log(baseConverter(100345, 2)); // 11000011111111001
console.log(baseConverter(100345, 8)); // 303771
console.log(baseConverter(100345, 16)); // 187F9
console.log(baseConverter(100345, 35)); // 2BW0
````
