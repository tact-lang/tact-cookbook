# Tact Cookbook

The core reason for creating the Tact Cookbook is to collect all the experience from Tact developers in one place so that future developers will use it!

Compared to the FunC Documentation, this article is more focused on everyday tasks every FunC developer resolve during the development of smart contracts.

## Basics
### How to write a Hello World smart contract

```
import "@stdlib/deploy";

contract SendEntireBalance with Deployable {
    const StorageFee: Int = ton("0.01");
    init(){}sd

    // We need empty receive method for possibility
    // to send coins without a message description
    receive(){}

    // Withdraw all coins from balance
    receive("withdraw entire balance"){
        let ctx: Context = context();
        send(SendParameters{to: ctx.sender, bounce: true, value: 0, mode: SendIgnoreErrors + SendRemainingBalance});
    }

    // Withdraw all coins from the balance,
    // but leave a minimum amount for contract rent.
    receive("withdraw entire balance safe"){
        let ctx: Context = context();
        send(SendParameters{to: ctx.sender,
                bounce: true,
                value: myBalance() - ctx.value - self.StorageFee,
                mode: SendIgnoreErrors + SendRemainingValue
            }
        );
    }

    get fun balance(): Int {
        return myBalance();
    }
}
```

