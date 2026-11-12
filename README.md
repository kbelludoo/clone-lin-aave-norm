# clone-lin-aave-norm

Experimental i64-positive LIN clone of Aave V3 `getNormalizedIncome` /
`getNormalizedDebt` (RAY'=1e9, explicit `dt`, 128-bit). **Not** mainnet
uint256 / RAY=1e27 / aToken parity.

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** (`examples/aave_norm/`, `make aave-norm-proof`).
This repository is the LIN copy only.

- Kernel: `src/lin_aave_norm.lin`
- Independent C11 oracle (not TCB): `test/oracles/aave_norm_c11.c`
- Upstream pin (hash-only, Solidity **not** vendored): `aave/aave-v3-core` `782f51917056a53a2c228701058a6c3fb233684a`
  - `contracts/protocol/libraries/logic/ReserveLogic.sol` sha256 `6b827ea494fa5bb1b38fa9e7db973bd0aed0ee3d53677cac950f6614cb8fd0c9` git blob `bc48163dbbfcac7c832d2e9dfef71a9ddadfe836`
  - `contracts/protocol/libraries/math/MathUtils.sol` sha256 `7f73c927e9801debfe0666e2a6364b92f62fd2d58d0c4b485ff04765fd4dc58d` git blob `9adca939db36cbe1009d0a00600def9314fc7332`
  - MIT after BUSL Change Date 2023-01-27
- Named goldens: `income(5e7, RAY', 1y) → 1050000000`; `income(5e7, RAY', 0) → RAY'` (same-block short-circuit); `income(5e7, RAY', 1d) → 1000136986`; typical 5% APR binomial extra terms floor to 0 at this scale; `compound(1e12, 1y) → 498260632232000` vs linear `1001000000000`.

Not claimed: aToken / pool parity, TVL savings, replacing Aave or the EVM, zk soundness, `rayMul`/`wadMul`/IRM (separate clone-lin repos).
