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
class Stack {
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
     * {2} IF the stack is not empty, we will decrement the count property
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

