# Array Notes | Data Structures

### Accessing elements and iterating an Array

````javascript
const fibonacci = [];

fibonacci[1] = 1;
fibonacci[2] = 2;

for (let i = 3; i < 20; i++) {
	fibonacci[i] = fibonacci[i - 1] + fibonacci[i - 2];
}

for (let i = 1; i < fibonacci.length; i++) {
	console.log(fibonacci[i]);
}
````

### Adding elements

#### Insert an element at the end of the array

````javascript
let numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

numbers[numbers.length] = 10;
````

#### Insert an element in the first position

````javascript
let numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

Array.prototype.insertFirstPosition = function(value) {
    for (let i = this.length; i >= 0; i--) {
        this[i] = this[i - 1];
    }

    this[0] = value;
};

numbers.insertFirstPosition(-1);
numbers.insertFirstPosition(-2);
````

#### Insert an element in the first position using the <u>unshift</u> method

````javascript
let numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

numbers.unshift(-1);
numbers.unshift(-2, -3);
````

### Removing elements

#### Remove an element from the end

````javascript
let numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

number.pop();
````

#### Remove and element from the first position

````javascript
let numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

Array.prototype.reIndex = function(myArray) {
    const newArray = [];
    for (let i = 0; i < myArray.length; i++) {
        if (myArray[i] !== undefined) {
            newArray.push(myArray[i]);
        }
    }

    return newArray;
}

Array.prototype.removeFirstPosition = function() {
    for (let i = 0; i < this.length; i++) {
        this[i] = this[i + 1];
    }
    return this.reIndex(this);
}

numbers = numbers.removeFirstPosition();
````

#### Remove and element from the first position by implementing the shift method

````javascript
let numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

numbers.shift();
````

#### Removing elements from a specific position 

````javascript
let numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

/**
 * @param 1 index of the array
 * @param 2 number of elements to remove
 **/

numbers.splice(5, 3);
````

> We should always use the `splice`, `pop`, `shift` methods to remove elements

#### Adding elements from a specific position

````javascript
/* Insert numbers 2 to 4 back into the array, starting grom position 5 */

/**
 * @argument [1] | Index we want to remove or insert elements into.
 * @argument [2] | The number of elements we want to remove, 0 to remove any.
 * @argument [3, 4, 5] |  The values we would like to insert
 **/
numbers.splice(5, 0, 2, 3, 4);

/* Adding and removing */
numbers.splice(5, 3, 2, 3, 4);
````



# References for JavaScript array methods

#### Joining multiple arrays

##### [concat] method

````javascript
const zero = 0;
const positiveNumbers = [1, 2, 3];
const negativeNumbers = [-3, -2, -1];
let numbers = negativeNumbers.concat(zero, positiveNumbers);
// Output: [ -3, -2, -1, 0, 1, 2, 3 ]
````

#### Iterator functions

````javascript
//returns true if x is a multiple of 2
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15];
const isEven = x => x % 2 === 0;
````

##### [every] method

> The `every` method iterates each element of the array until the function returns `false`.

````javascript
numbers.every(isEven);
// Output: false
````

##### [some] method

> The `some` method iterates each element of the array until the function returns `true`.

````javascript
numbers.some(isEven);
// Output: true
````

##### [forEach] method

> The `forEach` function has the same result a using a for loop.

````javascript
numbers.forEach(x => console.log(x % 2 === 0));
// Output: false, true, ...
````

##### [map] method

> Creates a new array from a function that contains the criterion/condition and returns the elements of the array that match the criterion

````javascript
const myMap = numbers.map(isEven);
````

##### [filter] method

> Creates an array with each element that evalutates to true in the function provided

````javascript
const evenNumbers = numbers.filter(isEven);
````

##### [reduce] method

The `reduce` method receives a function with the following parameters: `previousValue`, `currentValue`, `index`, and `array`. The `index` and array are optional parameters, so we do not need to pass them if we do not need to use them.

````javascript
numbers.reduce((previous, current) => previous + current);
// Output: 120
````

#  ES6 new array functionalities

#### Iterating using the for...of loop

````javascript
for (const n of numbers) {
    console.log(n % 2 === 0 ? 'even' : 'odd');
}
````

#### Using the @@iterator object

````javascript
// let iterator = numbers[Symbol.iterator]();
for (const n of iterator) {
    console.log(n);
}
````

#### Array entries method

````javascript
let aEntries = numbers.entries();
for (const n of aEntries) {
    console.log(n);
}
````

#### Array keys method

````javascript
let aKeys = numbers.keys();
console.log(aKeys.next()); // { value: 0, done: false }
console.log(aKeys.next()); // { value: 1, done: false }
````

#### Array values method

````javascript
const aValues = numbers.values();
console.log(aValues.next()); // { value: 1, done: false }
console.log(aValues.next()); // { value: 1, done: false }
````

#### Array from method

````javascript
let evens = Array.from(numbers, x => (x % 2 == 0));
````

#### Array of method

````javascript
let numbers3 = Array.of(1);
let numbers4 = Array.of(1, 2, 3, 4);
let numbersCopy = Array.of(...numbers4);
````

#### Array fill method

````javascript
let numbersCopy = Array.of(1, 2, 3, 4, 5, 6);
numbersCopy.fill(0);
````
> The fill method is great when we want to create an array and initialize its values, as demostrated.

```` javascript
let one = Array(6).fill(1);
````

### Sorting elements

````javascript
numbers.sort((a, b) => a - b);
console.log(numbers);
````

> The `sort` function from the JavaScript `Array` class can receive a parameter called `compareFunction`

#### Custom sorting

````javascript
const friends = [
    { name: 'John', age: 30 },
    { name: 'Ana', age: 20 },
    { name: 'Chris', age: 25 }, // trailing comma ES2017
];

function comparaPerson(a, b) {
    if (a.age < b.age) {
        return -1;
    }
    if(a.age > b.age) {
        return 1;
    }
    return 0;
}

console.log(friends.sort(comparaPerson));
````

#### Sorting strings

````javascript
let names = ['Ana', 'ana', 'john', 'John'];
console.log(names.sort());
// Output: [ 'Ana', 'John', 'ana', 'john' ]
````

> JavaScript compares each character according to its **ASCCI** value.

````javascript
let names = ['Ana', 'ana', 'john', 'John'];
console.log( names.sort((a, b) => {
    if (a.toLocaleLowerCase() < b.toLocaleLowerCase()) {
        return -1;
    }

    if (a.toLocaleLowerCase() > b.toLocaleLowerCase()) {
        return 1;
    }
    return 0;
}));
````

> If we want lowercase letters to come first in the sorted array, then we need to use the `localCompare` method

````javascript
names.sort((a, b) => a.localeCompare(b))
````

> FOr accented characters we ca use the `localeCompare` method as well.

````javascript
const names2 = ['Maève', 'Maeve'];
console.log(names2.sort((a, b) => a.localeCompare(b)));
````

### Searching

````javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15];
function multipleOf13(element, index, array) {
  return (element % 13 == 0);
}

console.log(numbers.find(multipleOf13)); 
console.log(numbers.findIndex(multipleOf13));
````

> The `find` method eturns the irst valueof the array that satisfies the proposed condition.

> The `findIndex` returns the index of the first value of the array

