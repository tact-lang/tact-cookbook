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

### How to write a do until loop

When we need the cycle to run at least once, we use `do until`.

```tact 
let flag: Bool = false;

do {
    // do something even flag is false
} until (flag);
```

> 💡 Useful links
> 
> ["Until loop" in docs](https://docs.tact-lang.org/language/guides/statements#until-loop)
> [Loops in Tact-By-Example](https://tact-by-example.org/04-loops)