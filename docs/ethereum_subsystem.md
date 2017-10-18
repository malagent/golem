# Ethereum Subsystem

## Modules

1. Ethereum Account
   Manages the password-protected Ethereum account private key.

2. Payment Sender
   Responsible for sending scheduled payments to Ethereum network.

3. Payment Monitor
   Responsible for monitoring, confirming and matching incoming payments
   with expected incomes.

4. Balance Manager?
   Capable of transfering tokens (GNT, ETH) by user request.

## Ethereum Account

The common solution is to keep the private key in a JSON file following
the [Web3 Secret Storage Definition] specification. There are at least 2 Python
implementations of this spec.

To sign an Ethereum transaction the account must be unlocked with
a user-provided password. There are multiple alternative scenarios how to handle
this problem.

### Unlock on startup

The password must be provided when Golem Client starts and the Ethereum Account
is unlocked all the time the Client is running. Payment Sender is able to sign
transaction without user attention.

### Unlock by UI when needed

The Ethereum Account module can provide a function to check whenever the account
is unlocked. The UI is responsible for unlocking the account if wants to perform
an action that requires signing Ethereum transactions. The account may be locked
again after some period of time.

This solution suffers from race conditions.

### Unlock on demand

The Ethereum Account module executes a callback function asking for password
when signing transaction is required. The callback is implemented by UI.
The account may be locked again after some period of time.


[Web3 Secret Storage Definition] https://github.com/ethereum/wiki/wiki/Web3-Secret-Storage-Definition
