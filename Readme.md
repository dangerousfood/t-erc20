# Transient Store ERC20 (TERC20)

This is a `TSTORE` version of ERC-20 implemented using a low iq search and replace on the [Solady](https://github.com/Vectorized/solady) ERC-20 implementation replacing the allowance `SSTORE` and `SLOAD` with `TSTORE` and `TLOAD`.

A foundry template with custom `solc` binaries (from [transient-storage](https://github.com/ethereum/solidity/tree/transient-store)) that supports transient storage opcodes in inline assembly.
```bash
forge build --use bin/solc
forge test  --use bin/solc
```

# Why?

Arguably that the design for `approve` and `allowance` within the ERC-20 standard is necessary, but it creates a significant attack surface for unrevoked approvals. 

The design is meant to create approvals that only last for the duration of the transaction. If TERC-20 were to be combined with an [EIP-4337](https://eips.ethereum.org/EIPS/eip-4337) wallet, we could create a safe `approve/allowance` system for users, without the need to revoke approvals.
