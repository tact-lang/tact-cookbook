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

💡 Useful links
- [`empty()` in docs](https://docs.tact-lang.org/language/ref/cells#sliceempty)
- [`dataEmpty()` in docs](https://docs.tact-lang.org/language/ref/cells#slicedataempty)
- [`refsEmpty()` in docs](https://docs.tact-lang.org/language/ref/cells#slicerefsempty)
- [`emptyCell()` in docs](https://docs.tact-lang.org/language/ref/cells#emptycell)