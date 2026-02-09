# Discoveries so far

- checked on openzepellin repo, and on `master` they are using `hardhat@2.28.0` - that uses `edr@0.12.0-next.17`
- EDR updated `revm` version on `0.12.0-next.18`
- Hardhat skipped `next.18` and integrated `next.19` directly on:
  - `2.28.1`
  - `3.1.1`
- Script fails as well using `hardhat@3.1.0`
- The impersonation of the address seem to be working ok, since if not EDR would be failing with `Unknown account error`
- The transaction is sent with the right `from` address
- When executing the `ContractWithFailingCall.lowLevelCallThenEventEmit` the transaction has 2 logs associated. One that is emitted by that contract, and the other by the caller contract (the contract at entrypoint address)
- When executing the `ContractWithFailingCall.lowLevelCall` the entrypoint contract is not emitting the log, so it would seem like the caller contract call is not being executed
- When executing the `ContractWithFailingCall.lowLevelDoubleCall` (that has two pop(call(..)) invocations), then the script works correctly and the entrypoint contract does emit two log entries
 - This makes me think that it’s an execution problem - not an instrumentation issue - because if not I think it should still fail with two consecutive `call`s
