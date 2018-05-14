###############################
Testing
###############################

With Stratis Smart Contracts, your tests can be developed and debugged using C# inside Visual Studio. The tests as described here verify that your smart contract logic executes as intended, before you deploy it to a live network.

.. note::
  Testing of Stratis Smart Contracts is still primitive. Future versions of smart contracts will enable testing with the resource tracking code injected, and on top of a local test blockchain.

The Basics
----------

This section will again reference the `Stratis Smart Contracts Visual Studio Template <https://marketplace.visualstudio.com/items?itemName=StratisGroupLtd.StratisSmartContractsTemplate>`_.

The tests inside the template use the ``Microsoft.VisualStudio.TestTools.UnitTesting`` library, so may be familiar to C# developers. A brief introduction:

- ``[TestClass]`` defines a class in which tests are defined.
- ``[TestInitialize]`` is used to mark a method to be run before tests execute, most commonly to set up some testing context.
- ``[TestMethod]`` marks the actual tests to be run.
- The static class ``Assert`` provides access to a range of methods to validate the results of whatever execution you perform inside your tests.

To run all of the tests together, in Visual Studio right click on ``[TestClass]`` and select `Run Tests`. To run tests individually, right click on the individual method and select `Run Tests`. Once clicked, the solution will take a couple of seconds to build and then the Test Explorer will open. You should see your tests listed next to a green tick indicating they've passed.

You can also debug contract execution in Visual Studio. If you set breakpoints in the Auction contract in methods being tested, and then right click and select `Debug Tests` on the test methods, you will reach your breakpoint and be able to inspect the current state of the contract and step through execution just like you were debugging any other C# application.

An Example
----------

Stepping through the `TestBidding()` method from the template should help you understand the rough approach to unit testing your contracts with a mock contract state.

::

  var auction = new Auction(SmartContractState, Duration);

The first step to testing your contracts is initialising them. You'll note that we're injecting a ``TestSmartContractState`` object into our new ``Auction``. This ``TestSmartContractState`` object is an implementation of the same ``ISmartContractState`` interface that is injected when smart contracts are initialised on-chain, except in this case all of the properties can be set by you.
This is really handy for you to explicitly target scenarios in your contract's execution.

::

  Assert.IsNull(SmartContractState.PersistentState.GetObject<Address>("HighestBidder").Value);
  Assert.AreEqual(0uL, SmartContractState.PersistentState.GetObject<ulong>("HighestBid"));

These calls check that the world state is as we expect after contract instantiation. Namely that no highest bidder has yet been set, and the current highest bidder is set to 0, which is exactly what the constructor is set to do.

::
  ((TestMessage)SmartContractState.Message).Value = 100;

  auction.Bid();

The first line here is an example of setting the state to represent exact scenarios that you wish to test.
