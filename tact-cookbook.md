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
let cell_with_data_and_refs: Cell  = beginCell().
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
