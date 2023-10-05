# Tact Cookbook

The core reason for creating the Tact Cookbook is to collect all the experience from Tact developers in one place so that future developers will use it!

Compared to the FunC Documentation, this article is more focused on everyday tasks every FunC developer resolve during the development of smart contracts.

## Basics
### How to send a message with the entire balance
If we need to send the entire balance of the smart contract, then, in this case, we need to use send `mode 128`. Another way we can use the mode `SendRemainingBalance`, which means the same thing.

```
send(SendParameters{
    to: ctx.sender, 
    value: 0, 
    mode: 128,
    bounce: true
});
```

> 💡 Useful links
> 
> ["Sending messages" in docs](https://docs.tact-lang.org/language/guides/send#send-message)
>
> ["Message modes" in docs](https://docs.tact-lang.org/language/ref/message-modes)