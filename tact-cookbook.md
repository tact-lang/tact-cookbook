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

## Loops
### How to write a while loop

While is useful when we do not know how often to perform a particular action.For example, there is a sickness spreading in our country, and we want to calculate how many days it would take for the population to die off.


```tact
// First, we define a constant variable called POPULATION to store the population size.
const POPULATION: Int = 42;

// Next, we create two variables to keep track of the number of newly sick and total sick people.
let newly_sick: Int = 0;
let total_sick: Int = 0;

// We will now start a loop to continue until the total number of sick people is less than the population size.
while (total_sick < POPULATION) {   

    // Every day, the total number of new sick people doubles.
    newly_sick = newly_sick * 2;
    
    // We update the total number of sick people by adding the newly sick people.
    total_sick = total_sick + newly_sick;

    // We increment the number of days.
    days = days + 1;
}

// We print the number of days it took for the entire population to get sick.
dump(days)

```

💡 Useful links

- [`while-loop` in docs](https://docs.tact-lang.org/language/guides/statements#while-loop)
- [`tact-by-example.org` @Loops](https://tact-by-example.org/04-loops)
- [`constants` in docs](https://docs.tact-lang.org/language/guides/constants)

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