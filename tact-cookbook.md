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

value: Int = 9001;

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
### How to convert int to string

```tact
let i1: Int = -12345;
let i2: Int = 6780000000; // coins = ton("6.78")

// Convert the Int value to a String.
// The value of s1 is "-12345".
let s1: String = i1.toString();

// Convert the Fixed Float value represented as an Int to a String.
// The parameter `digits` (3 in this example) determines the precision of the float number.
// The valid range for `digits` is 0 <= digits < 77.
// The value of s2 is "-12.345".
let s2: String = i1.toFloatString(3);

// Convert the nanoToncoin Int value to a String representing a float number of Toncoins and return it.
// The value of s3 is "6.78".
let s3: String = i2.toCoinsString();
```

> 💡 Useful links
>
> [`Int.toString` in docs](https://docs.tact-lang.org/language/ref/strings#inttostring)
>
> [`Int.toFloatString` in docs](https://docs.tact-lang.org/language/ref/strings#inttofloatstring)
>
> [`Int.toCoinsString` in docs](https://docs.tact-lang.org/language/ref/strings#inttocoinsstring)
>
> [`Strings` in Tact-By-Example](https://tact-by-example.org/02-strings)

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
