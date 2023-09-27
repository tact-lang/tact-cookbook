# Tact Cookbook

The core reason for creating the Tact Cookbook is to collect all the experience from Tact developers in one place so that future developers will use it!

Compared to the FunC Documentation, this article is more focused on everyday tasks every FunC developer resolve during the development of smart contracts.

## Basics
### How to send a message with a long text comment

If we need to send a message with a long text comment, we should build a string that consist more than `127` chars. For this we can use the primivite type `StringBuilder` and it's methods `beginComment()` and `append`. Before sending, we should convert this string into the cell with `toCell()` method.

```
let comment: StringBuilder = beginComment();
let longString = '...' // some string with amount of chars more than 127
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

