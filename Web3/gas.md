# Demystifying Gas in Blockchain Transactions

## Gas Price: Akin to Gasoline Prices

Understanding gas in blockchain transactions is akin to grasping the concept of gasoline prices when fueling up your car. At the gas station, the displayed price per liter guides your decision on how much money you'll spend.

In the blockchain world, the `gas price` mirrors this idea. Just as you consider the cost of each liter of gasoline, users assess the price of each unit of gas when conducting transactions.

Consider this analogy: When you fill up your car, the total cost is calculated as follows:

```txt
gasoline price * liters filled = total cost
```

For instance, if the gasoline price is $3 per liter and you fill up 10 liters, your total cost would be $3 \* 10 = $30.

## Deciphering Transaction Fees

But how does this translate to blockchain transactions?

In blockchain transactions, we replace liters with the concept of `gaslimit & Usage by Txn`.

- `Gas Limit`: The maximum gas the transaction may cost.
- `Usage by Txn`: The actual gas consumed during the transaction.

The total fee is then determined by the formula:

```txt
gas price * usage by txn = total fee
```

Lets break down a transaction example to illustrate([view full list](https://sepolia.etherscan.io/tx/0x4b7ed73abdfcdb06d90dcd06af3c7802959db9acff8381e046aca7e74ede38a3)):

| property                 | data                                                                    |
| ------------------------ | ----------------------------------------------------------------------- | ------------- |
| Transaction Fee          | 0.000031500000273 ETH                                                   |
| Gas Price                | 1.500000013 Gwei (0.000000001500000013 ETH)                             |
| Gas Limit & Usage by Txn | 21,000                                                                  | 21,000 (100%) |
| Gas Fees                 | Base: 0.000000013 Gwei \|Max: 1.500000018 Gwei \|Max Priority: 1.5 Gwei |

In this example, the transaction fee is calculated as `1.500000013 Gwei * 21000 = 31500.000273 Gwei`, equivalent to `0.000031500000273 ETH`. You can use the [Ethereum Unit Converter](https://eth-converter.com/) for easy conversion.

You may notice we have not explained how the `Gas Price` is calculated yet. let's delve into the calculation of the Gas Price by understanding the components of the Gas Fee section:

1. Base: the network base fee at the time of the block.The base fee is dynamic and changes based on the network's congestion. Higher demand for transactions leads to an increase in the base fee. It is a reflection of the cost of computational resources in the network.
2. Max: the max amount a user is willing to pay for the transaction.Users specify the maximum gas price they are willing to pay for each unit of gas in the transaction. It acts as an upper limit to control costs.
3. Max Priority: The maximum tip price a user is willing to pay for the transaction.This represents an additional incentive for miners or block producers. A higher max priority means the user is willing to pay a premium for quicker execution of the transaction.

Determining the Gas Price in blockchain transactions involves a bit of a dynamic dance, thanks to the ever-changing base fee.

The standard formula is simple:

```txt
max priority + base fee = gas price
```

However, with the base fee being as capricious as the wind, predicting it at the exact moment of transaction execution becomes a bit of a challenge.

Enter Metamask, your trusty companion in the crypto realm. Metamask takes a proactive approach by providing a gas fee slightly higher than the estimated fee. But here's where it gets interesting— in the advanced gas fee settings, you have the power to set a max base fee. This essentially lets you establish the maximum base fee you're willing to dish out.

So, the refined formula for calculating the gas fee becomes:

```txt
max priority + current base fee = gas fee
```

It's like setting a budget for tolls on a highway that fluctuates based on real-time traffic conditions.

In the above transaction, the gas price is calculated in the following formula:

```txt
// base + max priority = gas price
0.000000013Gwei + 1.5Gwei = 1.500000013Gwei
```

`1.500000013Gwei` is the final gas price, the **per unit** price, similar to the gasoline price per liter.

Now we know how the transaction fee is calculated out.
