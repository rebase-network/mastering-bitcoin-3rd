# 确定合适的费率估算

我们已经确定，如果你愿意等待更长的时间来确认你的交易，你可以支付较低的费率，但要注意支付过低的费率可能导致你的交易永远无法确认。由于费率是对区块空间的一个开放拍卖的出价，所以无法完全预测你需要支付多少费率才能在特定时间内确认你的交易。然而，我们可以根据最近其他交易所支付的费率来生成一个粗略的估算。&#x20;

一个完整的节点可以记录每个交易的三个信息：它首次收到该交易的时间（区块高度）、该交易被确认的区块高度以及该交易支付的费率。通过将到达时间相似、确认时间相似且支付费率相似的交易分组在一起，我们可以计算确认支付某一费率的交易需要多少个区块。然后，我们可以假设现在支付类似费率的交易将需要相似数量的区块来确认。Bitcoin Core包含一个使用这些原理的费率估算器，可以使用`estimatesmartfee` RPC调用，参数指定在交易高度高度可能确认之前你愿意等待多少个区块（例如，144个区块约为1天）：

```
$ bitcoin-cli -named estimatesmartfee conf_target=144
{
 "feerate": 0.00006570,
 "blocks": 144
}
```

\
许多基于网络的服务也提供作为API的费率估算。当前列表请参见https://oreil.ly/TB6IN。

如前所述，费率估算永远不可能完美无缺。一个常见的问题是基本需求可能会发生变化，调整均衡点，将价格（费用）提高到新的高度，或者将其降低到最低水平。如果费率下降，那么以前支付正常费率的交易现在可能支付较高的费率，并且将比预期更早地得到确认。对于您已经发送的交易，无法降低费率，因此您将被困在支付更高费率的情况下。但是，当费率上升时，有必要采取方法来增加这些交易的费率，这称为费率提升。比特币中常用的两种费率提升方法是替换交易（RBF）和子付费（CPFP）。