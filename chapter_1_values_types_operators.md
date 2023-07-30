#### Chapter 1

# Values, Types and Opeators

[Eloquent Javascript Chapter 1 Link](https://eloquentjavascript.net/01_values.html)

### Unary Operations

The **typeof** takes only one value. Operators that take two values are called _binary_ Operators, while those take one are called _Unary_ Operators. The - operator can be used both as a binary operator and unary operator.

### Logical Opeators

The **&&** operator represents logical _and_. It is a binary operator, and its result is true only if both the values given to it are true.

```javascript
console.log(true && false);
// → false
console.log(true && true);
// → true
```

The || operator denotes logical or. It produces true if either of the values given to it is true.

```javascript
console.log(false || true);
// → true
console.log(false || false);
// → false
```

Not is written as an exclamation mark (!). It is a unary operator that flips the value given to it—!true produces false, and !false gives true.

When mixing these Boolean operators with arithmetic and other operators, it is not always obvious when parentheses are needed. In practice, you can usually get by with knowing that of the operators we have seen so far, || has the lowest precedence, then comes &&, then the comparison operators (>, ==, and so on), and then the rest.

The last logical operator I will discuss is not unary, not binary, but ternary, operating on three values. It is written with a question mark and a colon, like this:

```javascript
console.log(true ? 1 : 2);
// → 1
console.log(false ? 1 : 2);
// → 2
```

This one is called the conditional operator (or sometimes just the ternary operator since it is the only such operator in the language). The value on the left of the question mark “picks” which of the other two values will come out. When it is true, it chooses the middle value, and when it is false, it chooses the value on the right.

### Empty values

There are two special values, written null and undefined, that are used to denote the absence of a meaningful value. They are themselves values, but they carry no information.

Many operations in the language that don’t produce a meaningful value (you’ll see some later) yield undefined simply because they have to yield some value.

The difference in meaning between undefined and null is an accident of JavaScript’s design, and it doesn’t matter most of the time. In cases where you actually have to concern yourself with these values, I recommend treating them as mostly interchangeable.

### Automatic type conversion

In the Introduction, I mentioned that JavaScript goes out of its way to accept almost any program you give it, even programs that do odd things. This is nicely demonstrated by the following expressions:

```javascript
console.log(8 * null);
// → 0
console.log("5" - 1);
// → 4
console.log("5" + 1);
// → 51
console.log("five" * 2);
// → NaN
console.log(false == 0);
// → true
```

When an operator is applied to the “wrong” type of value, JavaScript will quietly convert that value to the type it needs, using a set of rules that often aren’t what you want or expect. This is called type coercion. The null in the first expression becomes 0, and the "5" in the second expression becomes 5 (from string to number). Yet in the third expression, + tries string concatenation before numeric addition, so the 1 is converted to "1" (from number to string).

When comparing values of the same type using ==, the outcome is easy to predict: you should get true when both values are the same, except in the case of NaN. But when the types differ, JavaScript uses a complicated and confusing set of rules to determine what to do. In most cases, it just tries to convert one of the values to the other value’s type. However, when null or undefined occurs on either side of the operator, it produces true only if both sides are one of null or undefined.

```javascript
console.log(null == undefined);
// → true
console.log(null == 0);
// → false
```

That behavior is often useful. When you want to test whether a value has a real value instead of null or undefined, you can compare it to null with the == (or !=) operator.

But what if you want to test whether something refers to the precise value false? Expressions like 0 == false and "" == false are also true because of automatic type conversion. When you do not want any type conversions to happen, there are two additional operators: === and !==. The first tests whether a value is precisely equal to the other, and the second tests whether it is not precisely equal. So "" === false is false as expected.

I recommend using the three-character comparison operators defensively to prevent unexpected type conversions from tripping you up. But when you’re certain the types on both sides will be the same, there is no problem with using the shorter operators.

### Short-circuiting of logical operators

The logical operators && and || handle values of different types in a peculiar way. They will convert the value on their left side to Boolean type in order to decide what to do, but depending on the operator and the result of that conversion, they will return either the original left-hand value or the right-hand value.

The || operator, for example, will return the value to its left when that can be converted to true and will return the value on its right otherwise. This has the expected effect when the values are Boolean and does something analogous for values of other types.

```javascript
console.log(null || "user");
// → user
console.log("Agnes" || "user");
// → Agnes
```

We can use this functionality as a way to fall back on a default value. If you have a value that might be empty, you can put || after it with a replacement value. If the initial value can be converted to false, you’ll get the replacement instead. The rules for converting strings and numbers to Boolean values state that 0, NaN, and the empty string ("") count as false, while all the other values count as true. So 0 || -1 produces -1, and "" || "!?" yields "!?".

The && operator works similarly but the other way around. When the value to its left is something that converts to false, it returns that value, and otherwise it returns the value on its right.

Another important property of these two operators is that the part to their right is evaluated only when necessary. In the case of true || X, no matter what X is—even if it’s a piece of program that does something terrible—the result will be true, and X is never evaluated. The same goes for false && X, which is false and will ignore X. This is called short-circuit evaluation.

The conditional operator works in a similar way. Of the second and third values, only the one that is selected is evaluated.
