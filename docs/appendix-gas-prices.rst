###############################
Appendix - Gas Prices
###############################

Smart contract execution costs the gas price (in satoshis) multiplied by the gas used. The gas price and the maximum amount of gas to be used are set at the transaction level.

For most transactions we would recommend setting your gas price to 1 and the gas limit to 100000.

* **Gas Price:** Minimum: 1. Maximum: 10000.
* **Gas Limit:** Minimum: 1000. Maximum: 5000000.

.. note::
  While the below gas prices are experimental and subject to change, we expect that the cost to deploy and interact with contracts will always be between 5c and $5 USD.

.. csv-table:: Gas Prices
  :header: "Operation", "Cost", "Description"

  Base Cost, 1000, Cost for executing any smart contract transaction
  Contract Creation Cost, 1000, Cost for creating a new contract
  Instruction Cost, 1, Cost for executing each CIL instruction
  System Method Call Cost, 0, Cost for calling any system method.
  Storage Cost (byte), 1, Cost for storing 1 byte via PersistentState. Includes keys and values.
