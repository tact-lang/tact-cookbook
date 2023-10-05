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

## Slice
### How to determine if slice is empty

`Slice` is considered *empty* if it has no stored `data` **and** no stored `references`.

Use `empty()` method to check if `slice` is empty.

```tact
// Create an empty slice with no data and no refs
let empty_slice: Slice = emptyCell().asSlice();
// Returns `true`, because slice doesn't have any `bits` and `refs`
empty_slice.empty();

// Create a slice with some data
let slice_with_data: Slice = beginCell().
    storeUint(42, 8).
    asSlice();
// Returns `false`, because slice have any `data`
slice_with_data.empty();

// Create a slice with reference to empty cell
let slice_with_refs: Slice  = beginCell().
    storeRef(emptyCell()).
    asSlice();
// Returns `false`, because slice have any `refs`
slice_with_refs.empty();

// Create a slice with data and reference
let slice_with_data_and_refs: Slice  = beginCell().
    storeUint(42, 8).
    storeRef(emptyCell()).
    asSlice();
// Returns `false`, because slice have any `data` and `refs`
slice_with_data_and_refs.empty(); 
```

💡 Useful links
- [`empty()` in docs](https://docs.tact-lang.org/language/ref/cells#sliceempty)
- [`dataEmpty()` in docs](https://docs.tact-lang.org/language/ref/cells#slicedataempty)
- [`refsEmpty()` in docs](https://docs.tact-lang.org/language/ref/cells#slicerefsempty)
- [`emptyCell()` in docs](https://docs.tact-lang.org/language/ref/cells#emptycell)