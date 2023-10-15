# Tact Cookbook

The core reason for creating the Tact Cookbook is to collect all the experience from Tact developers in one place so that future developers will use it!

Compared to the FunC Documentation, this article is more focused on everyday tasks every FunC developer resolve during the development of smart contracts.

## Basics
### How to send a message with a long text comment

If we need to send a message with a lengthy text comment, we should create a string that consists of more than `127` characters. To do this, we can utilize the `StringBuilder` primitive type and its methods called `beginComment()` and `append()`. Prior to sending, we should convert this string into a cell using the toCell() method.

```
let comment: StringBuilder = beginComment();
let longString = '...' // Some string with more than 127 characters.
str_builder.append(longString);

send(SendParameters{
    to: ctx.sender, 
    value: 0, 
    mode: SendIgnoreErrors,
    body: longString.toCell(),
    bounce: true,
});
```

💡 Useful links

- ["Sending messages" in docs](https://docs.tact-lang.org/language/guides/send#send-message)
- ["String builder" in docs](https://docs.tact-lang.org/language/guides/types#primitive-types)
- ["Cell" in docs](https://docs.tact-lang.org/language/ref/cells)

