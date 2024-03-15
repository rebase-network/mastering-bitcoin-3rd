# 使用有损编码来减少带宽

\
我们希望在一个区块中传输的交易数据是输出脚本。输出脚本的长度各不相同，并且遵循不同的模式，这意味着它们之间的差异并不会像我们期望的那样均匀分布。然而，在本书的许多地方已经提到，我们可以使用哈希函数来创建对某些数据的承诺，并且还可以生成类似于随机选择的数字。在本书的其他地方，我们已经使用了一个具有密码学安全性的哈希函数，它提供了关于其承诺强度和其输出与随机性之间的不可区分性的保证。然而，还有一些更快速和更可配置的非密码学哈希函数，例如我们将用于紧凑块过滤器的SipHash函数。

所使用算法的详细信息在BIP158中有描述，但其要点是使用SipHash和一些算术运算将每个输出脚本简化为一个64位的承诺。您可以将其视为将一组大数字截断为较短数字的过程，这个过程会丢失数据（因此称为有损编码）。通过丢失一些信息，我们就不需要在后续存储那么多信息，从而节省空间。在这种情况下，我们从典型的长度为160位或更长的输出脚本减少到仅仅64位。