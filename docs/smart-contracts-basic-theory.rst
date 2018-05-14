###############################
Smart Contracts - Basic Theory
###############################

You may already have heard of DApps (Decentralized Apps). A smart contract can also be thought of as a DApp because it is both an application and is decentralized. In fact, DApps consist of a web-based front-end that sits on top of a smart contract. A DApp is decentralized because of the properties of the smart contract; a copy of the DApp’s smart contract is stored on each node in the blockchain.

Although a smart contract is stored on all nodes, it is important to remember they only need to be run by one node to accomplish their task. They are invoked when a transaction is added to a blockchain and usually affect the outcome of that transaction.

.. note::
    Given a specific input, the output of the smart contract is the same no matter which node it is run on. Because of this property, smart contracts are deterministic.

Smart contracts are also capable of storing (persisting) data. If they could not do this, it would be impossible for them to achieve the required level of sophistication. You might be asking a question at this point: if a smart contract is stored on every node in the blockchain but gets run on random nodes, what happens to any data it stores when running? The answer is that any data stored by a smart contract is broadcast across all nodes on the network. A smart contract on any node has up-to-date copies of its “database”.

Using .NET for smart contracts
------------------------------

The most important aspect of the implementation of Stratis smart contracts is they use “real” .Net, which is to say .Net Core is used to execute them. The Stratis Full Node is also written in C# and the route of execution for both it and and a Stratis smart contract is the same. Stratis smart contracts are not just using the C# syntax, they are using the full tried and tested C# package supplied by Microsoft.

Because smart contracts are deterministic, they cannot use all capabilities of the C# language or all the .Net Core libraries. The Stratis smart contracts suite includes a validation tool that checks for any non-deterministic elements in any smart contracts that you write.