Our Contract is on-chain, and we're going to learn how to fetch the data stored on the contract. 

{% hint style="info" %}
If you want to learn more about Tezos smart contracts, follow [**The Taco Shop Smart Contract**](https://ligolang.org/docs/tutorials/get-started/tezos-taco-shop-smart-contract) tutorial.
{% endhint %}

------------------------

# Challenge

{% hint style="tip" %}
In `pages/api/tezos/getter.ts`, implement the function and try to read the value of the counter stored in the smart contract. You must replace the instances of `undefined` with working code to accomplish this. 
{% endhint %}

**Take a few minutes to figure this out**

```typescript
//...
  try {
    const { mnemonic, email, password, secret, contract } = req.body;
    const url = getTezosUrl();
    const tezos = new TezosToolkit(url);

    await importKey(
      tezos,
      email,
      password,
      mnemonic,
      secret
    );

    // Use the contract module to get the storage
    const counter = undefined;

    // @ts-ignore
    res.status(200).json(counter.toString());
  } 
//...
```

**Need some help?** Check out these links
* [**Interface ContractProvider method `getStorage`**](https://tezostaquito.io/typedoc/interfaces/_taquito_taquito.contractprovider.html#getstorage)  

{% hint style="info" %}
You can [**join us on Discord**](https://discord.gg/fszyM7K), if you have questions or want help completing the tutorial.
{% endhint %}

Still not sure how to do this? No problem! The solution is below so you don't get stuck.

------------------------

# Solution

```typescript
//...
  try {
    const { mnemonic, email, password, secret, contract } = req.body;
    const url = getTezosUrl();
    const tezos = new TezosToolkit(url);

    await importKey(
      tezos,
      email,
      password,
      mnemonic,
      secret
    );

    const counter = await tezos.contract.getStorage(contract);

    // @ts-ignore
    res.status(200).json(counter.toString());
  } 
//...
```

**What happened in the code above?**

* First, we create a new `TezosToolkit` instance.
* Next, we import our wallet data using `importKey`.
* Then, using the `getStorage` function of the `contract` module, we return the counter stored on the contract.
* Finally, we send the `counter` value converted `toString` back to the client-side as JSON.

------------------------

# Make sure it works

Once you have the code above saved, click the button and watch the magic happen:

![](../../../.gitbook/assets/pathways/tezos/tezos-getter.gif)

-----------------------------

# Conclusion

Nicely done! You learned how to get a value from a smart contract's storage on the Tezos blockchain. Now it is time for the final challenge: Modify the state of the contract and thus the state of the blockchain. Let's go!
