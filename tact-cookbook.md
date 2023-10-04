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

### How to determine if slice is empty

`Slice` is considered *empty* if it has no stored `data` **and** no stored `references`.

Use `empty()` method to check if `slice` is empty.

To check if slice `data` is empty, use `dataEmpty()` method.

To check if slice `refs` is empty, use `refsEmpty()` method.

```tact
// Create an empty slice with no data and no refs
let empty_slice: Slice = emptyCell().asSlice();

empty_slice.dataEmpty(); // returns `true`
empty_slice.refsEmpty(); // returns `true`
empty_slice.empty();     // returns `true` 


// Create a slice with some data
let slice_with_data: Slice = beginCell().
    storeUint(42, 8).
    asSlice();

slice_with_data.dataEmpty(); // returns `false`
slice_with_data.refsEmpty(); // returns `true`
slice_with_data.empty();     // returns `false` 


// Create a slice with reference to empty cell
let slice_with_refs: Slice  = beginCell().
    storeRef(emptyCell()).
    asSlice();

slice_with_refs.dataEmpty(); // returns `true`
slice_with_refs.refsEmpty(); // returns `false`
slice_with_refs.empty();     // returns `false` 


let slice_with_data_and_refs: Slice  = beginCell().
    storeUint(42, 8).
    storeRef(emptyCell()).
    asSlice();

slice_with_data_and_refs.dataEmpty(); // returns `false`
slice_with_data_and_refs.refsEmpty(); // returns `false`
slice_with_data_and_refs.empty();     // returns `false` 
```

💡 Useful links

- [`empty()` in docs](https://docs.tact-lang.org/language/ref/cells#sliceempty)
- [`dataEmpty()` in docs](https://docs.tact-lang.org/language/ref/cells#slicedataempty)
- [`refsEmpty()` in docs](https://docs.tact-lang.org/language/ref/cells#slicerefsempty)

👀 See also

- ["Get number of references" in docs](https://docs.tact-lang.org/language/ref/cells#slicerefs)
- ["Get number of data bits" in docs](https://docs.tact-lang.org/language/ref/cells#slicebits)