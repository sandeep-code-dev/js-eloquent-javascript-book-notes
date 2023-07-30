#### Chapter 4

# Data Structures: Objects and Arrays

Numbers, Booleans, and strings are the atoms that data structures are built from. Many types of information require more than one atom, though. Objects allow us to group values—including other objects—to build more complex structures.

### Data sets

To work with a chunk of digital data, we’ll first have to find a way to represent it in our machine’s memory. Say, for example, that we want to represent a collection of the numbers 2, 3, 5, 7, and 11.

We could get creative with strings—after all, strings can have any length, so we can put a lot of data into them—and use "2 3 5 7 11" as our representation. But this is awkward. You’d have to somehow extract the digits and convert them back to numbers to access them.

Fortunately, JavaScript provides a data type specifically for storing sequences of values. It is called an array and is written as a list of values between square brackets, separated by commas.

```javascript
let listOfNumbers = [2, 3, 5, 7, 11];
console.log(listOfNumbers[2]);
// → 5
console.log(listOfNumbers[0]);
// → 2
console.log(listOfNumbers[2 - 1]);
// → 3
```

The notation for getting at the elements inside an array also uses square brackets. A pair of square brackets immediately after an expression, with another expression inside of them, will look up the element in the left-hand expression that corresponds to the index given by the expression in the brackets.

The first index of an array is zero, not one. So the first element is retrieved with listOfNumbers[0]. Zero-based counting has a long tradition in technology and in certain ways makes a lot of sense, but it takes some getting used to. Think of the index as the amount of items to skip, counting from the start of the array.
