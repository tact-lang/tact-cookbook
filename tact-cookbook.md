# Tact Cookbook

The core reason for creating the Tact Cookbook is to collect all the experience from Tact developers in one place so that future developers will use it!

Compared to the FunC Documentation, this article is more focused on everyday tasks every FunC developer resolve during the development of smart contracts.

## Basics

### How to write a Hello World smart contract

```
contract HelloWorld {
    get fun greeting(): String {
        return "hello world";
    }        
}
```

### How to write an 'if' statement in Tact

Tact supports `if` statements in a similar syntax to most programming languages. 
The condition of the statement can be any boolean expression.

```
let value: Int = 9001;

if (value > 10) {
    // do something
}

if (value > 100) {
    // do something
} else {
    // do something else
}

if (value > 9000) {
    // do something
} else if (value > 500) {
    // do another thing
} else {
    // do something else
}
```

## Loops

### How to write a repeat loop

Please make sure the input number for the repeat loop statement is within the range of an int32 data type, as an exception will be thrown otherwise.

```
let sum: Int = 0;
let i: Int = 0;

repeat (10) {               // repeat exactly 10 times
    i = i + 1;
    sum = sum + i;
}
```

### How to write a while loop 

```
let i: Int = 0;

while (i < 10) {
    i = i + 1;
}
```
💡 Useful links

- ["While loop" in docs](https://docs.tact-lang.org/language/guides/statements#while-loop)
- [Loops in Tact-By-Example](https://tact-by-example.org/04-loops)

### How to write a do until loop

When we need the cycle to run at least once, we use `do-until`.

```tact
let num: Int;               // A variable to store the random number

// A do until loop that repeats until num is equal to 5
do {
    num = random(0, 9);     // get a random number between 0 and 9
} until (num == 5);         // stop loop if num is equal to 5

dump("The loop is over!");
```

💡 Useful links
 
- [`do-until` in docs](https://docs.tact-lang.org/language/guides/statements#until-loop)
- [`random()` in docs](https://docs.tact-lang.org/language/ref/random#random)
- [`tact-by-example.org` @Loops](https://tact-by-example.org/04-loops)

## Strings

### How to convert string to int

```tact
// Dangerously casts string as slice for parsing. Use it only if you know what you are doing.
// Try to parse the string as an slice
let string: Slice = "26052021".asSlice();

// A variable to store the number
let number: Int = 0;

while (!string.empty()) {                   // A loop until slice has bytes
    let char: Int = string.loadUint(8);     // load slice bytes
    number = (number * 10) + (char - 48);   // we use ASCII table to get number
}

dump(number);
```

💡 Useful links
- [`while()` in docs](https://docs.tact-lang.org/language/guides/statements#while-loop)
- [`empty()` in docs](https://docs.tact-lang.org/language/ref/cells#sliceempty)
- [`loadUint()` in docs](https://docs.tact-lang.org/language/ref/cells#sliceloaduint)
- [`String.asSlice()` in docs](https://docs.tact-lang.org/language/ref/strings#stringasslice)

## Slice

### How to determine if slice is empty

`Slice` is considered *empty* if it has no stored `data` **and** no stored `references`.

Use `empty()` method to check if a `slice` is empty.

```tact
// Create an empty slice with no data and no refs
let empty_slice: Slice = emptyCell().asSlice();
// Returns `true`, because `empty_slice` doesn't have any data or refs
empty_slice.empty();

// Create a slice with some data
let slice_with_data: Slice = beginCell().
    storeUint(42, 8).
    asSlice();
// Returns `false`, because the slice has some data
slice_with_data.empty();

// Create a slice with a reference to an empty cell
let slice_with_refs: Slice  = beginCell().
    storeRef(emptyCell()).
    asSlice();
// Returns `false`, because the slice has a reference
slice_with_refs.empty();

// Create a slice with data and a reference
let slice_with_data_and_refs: Slice  = beginCell().
    storeUint(42, 8).
    storeRef(emptyCell()).
    asSlice();
// Returns `false`, because the slice has both data and reference
slice_with_data_and_refs.empty(); 
```

## Cell

### How to determine if a cell is empty

To check if there is any data in a `cell`, we should first convert it to `slice`. If we are only interested in having bits, we should use `dataEmpty()`, if only refs - `refsEmpty()`. In case we want to check for the presence of any data, regardless of whether it is a bit or ref, we need to use `empty()`.

```tact
// Create an empty cell with no data and no refs
let empty_cell: Cell = emptyCell(); // alias for beginCell().endCell()
// Present `cell` as a `slice` to parse it.
let slice: Slice = empty_cell.asSlice();
// Returns `true`, because `slice` doesn't have any data or refs
slice.empty();

// Create a cell with bits and references
let cell_with_data_and_refs: Cell = beginCell().
    storeUint(42, 8).
    storeRef(emptyCell()).
    endCell();
// Change `cell` type to slice with `begin_parse()`
let slice: Slice = cell_with_data_and_refs.asSlice();
// Returns `false`, because `slice` has both data and refs
slice.empty();
```

💡 Useful links

- [`empty()` in docs](https://docs.tact-lang.org/language/ref/cells#sliceempty)
- [`dataEmpty()` in docs](https://docs.tact-lang.org/language/ref/cells#slicedataempty)
- [`refsEmpty()` in docs](https://docs.tact-lang.org/language/ref/cells#slicerefsempty)
- [`emptyCell()` in docs](https://docs.tact-lang.org/language/ref/cells#emptycell)
- [`beginCell()` in docs](https://docs.tact-lang.org/language/ref/cells#begincell)
- [`endCell()` in docs](https://docs.tact-lang.org/language/ref/cells#builderendcell)

## Sending messages

### How to send a message with the entire balance

If we need to send the whole balance of the smart contract, then we should use the `SendRemainingBalance` send mode. Alternatively, we can use `mode 128`, which has the same meaning.

```
send(SendParameters{
    to: ctx.sender, 
    value: 0, 
    mode: SendRemainingBalance, // or mode: 128
    bounce: true
});
```

💡 Useful links
 
- ["Sending messages" in docs](https://docs.tact-lang.org/language/guides/send#send-message)
- ["Message modes" in docs](https://docs.tact-lang.org/language/ref/message-modes)
