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
### How to write a while loop 

```
// Initialize a variable 'i' of type Int and set its value to 0
let i: Int = 0;
// Print the numbers 0 through 9 using a while loop
while (i < 10) {
// Increment the value of 'i' by 1
   i = i + 1;
}

```
> 💡 Useful links
> 
> ["While loop" in docs](https://docs.tact-lang.org/language/guides/statements#while-loop)
> [Loops in Tact-By-Example](https://tact-by-example.org/04-loops)
