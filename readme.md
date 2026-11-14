# Solana Anchor Escrow

A trustless token escrow program on Solana, written in Rust with the Anchor framework. A maker locks token A and names the amount of token B they want in return; a taker completes the swap, or the maker cancels and gets their tokens back. Built as part of the Turbin3 Pre-Builder program.

**Status:** Educational project, not audited. Do not use with real funds.

## How it works

| Instruction | Who | What it does |
|-------------|-----|--------------|
| `make` | Maker | Initializes the escrow and locks the maker's token A |
| `take` | Taker | Executes the trade: swaps the assets between maker and taker, then closes the escrow state |
| `refund` | Maker | Cancels the escrow and returns the locked tokens to the maker |

The program makes Cross-Program Invocations (CPI) to the SPL Token program for transfers and account authority handling.

## Features

- Full escrow lifecycle: create (`make`), complete (`take`) and cancel (`refund`)
- Modular design with each instruction handler in its own module
- Secure token management through CPI with the SPL Token program
- TypeScript integration tests covering the core scenarios

## Tech stack

- Solana
- Anchor framework
- Rust
- TypeScript
- `@coral-xyz/anchor`
- `@solana/spl-token`
- `@solana/web3.js`

## Project structure

```
.
├── programs/
│   └── anchor-escrow/
│       ├── Cargo.toml
│       └── src/
│           ├── lib.rs            # Program entrypoint and routing
│           └── instructions/
│               ├── make.rs       # Initializes escrow, locks maker's tokens
│               ├── take.rs       # Executes the swap and closes state
│               └── refund.rs     # Cancels escrow, returns tokens to maker
├── Anchor.toml
└── README.md
```

The TypeScript integration tests are in `escrow.t.ts`.

## Getting started

### Prerequisites

- Rust and the Solana CLI
- Anchor CLI, using the version pinned in `Anchor.toml`
- Node.js and Yarn or npm

### Install

```bash
git clone https://github.com/Armaansaxena/Solana-anchor-escrow
cd Solana-anchor-escrow
npm install   
```

### Run the tests

```bash
anchor test
```

## Known limitations

- Not audited. This is a learning project.
- Single-trade escrows only: one maker, one taker and a fixed token pair per escrow.

## Author

Armaan Saxena. [GitHub](https://github.com/Armaansaxena)
