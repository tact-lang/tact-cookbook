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

### How to write a repeat loop

Tact does not support traditional for loops, but its loop statements are equivalent and can easily implement the same functionality. Also, note that Tact does not support the use of break and continue statements in loops, unlike some other programming languages.

Please ensure that the input number for the repeat loop statement is within the range of an int32 datatype, as an exception will be thrown otherwise.

```

    let sum: Int = 0;
    let i: Int = 0;
    repeat (10) {               // repeat exactly 10 times
        i = i + 1;
        sum = sum + i;
    }

```
