

# XpChain - Gamin Gaming Platform Smart Contract

A smart contract for managing gaming assets, ownership, transfers, marketplace listings, and player statistics on the Stacks blockchain using Clarity.

---

## 📜 Table of Contents

* [Overview](#overview)
* [Features](#features)
* [Smart Contract Architecture](#smart-contract-architecture)
* [Functions](#functions)

  * [Public Functions](#public-functions)
  * [Read-Only Functions](#read-only-functions)
* [Constants & Limits](#constants--limits)
* [Error Codes](#error-codes)
* [Setup & Deployment](#setup--deployment)
* [Example Usage](#example-usage)
* [License](#license)
* [Name Suggestions](#name-suggestions)

---

## 📖 Overview

The **Gamin Gaming Platform** smart contract enables secure and efficient in-game asset management and trading on the blockchain. It supports:

* Minting single or multiple in-game assets.
* Transferring ownership of assets.
* Listing assets on a marketplace.
* Purchasing assets using STX.
* Tracking player statistics like experience and level.

---

## ✨ Features

* ✅ Batch and single asset minting.
* 🔐 Ownership and transferability restrictions.
* 🏪 Built-in marketplace for buying/selling assets.
* 📊 Player stat tracking (experience, level).
* ⚙️ Batch operations with gas cost safeguards.
* 📎 Metadata URI validation for off-chain asset details.

---

## 🏗️ Smart Contract Architecture

The contract is structured around several key components:

### Maps

* `assets`: Stores all minted assets with owner, metadata, and transferability.
* `asset-prices`: (Currently unused — could be deprecated or extended).
* `marketplace-listings`: Assets listed for sale with price, seller, and timestamp.
* `player-stats`: Stores experience and level per player.

### Data Variables

* `asset-counter`: Tracks total assets minted.

### Constants

Predefined limits and error codes (detailed [below](#constants--limits)).

---

## 🛠️ Functions

### 🔓 Public Functions

| Function                                              | Description                                        |
| ----------------------------------------------------- | -------------------------------------------------- |
| `mint-asset(metadata-uri, transferable)`              | Mint a single asset (only contract owner).         |
| `batch-mint-assets(metadata-uris, transferable-list)` | Mint multiple assets at once (owner only, max 10). |
| `transfer-asset(asset-id, recipient)`                 | Transfer ownership of an asset.                    |
| `batch-transfer-assets(asset-ids, recipients)`        | Batch transfer multiple assets.                    |
| `list-asset-for-sale(asset-id, price)`                | List an asset for sale on the marketplace.         |
| `purchase-asset(asset-id)`                            | Purchase a listed asset with STX.                  |
| `delist-asset(asset-id)`                              | Remove an asset from sale.                         |
| `update-player-stats(experience, level)`              | Set player stats (level, XP).                      |

---

### 📖 Read-Only Functions

| Function                            | Description                                      |
| ----------------------------------- | ------------------------------------------------ |
| `get-asset-details(asset-id)`       | View asset metadata, owner, and transferability. |
| `get-marketplace-listing(asset-id)` | View asset's listing info (seller, price, etc.). |
| `get-player-stats(player)`          | View player’s XP and level.                      |
| `get-total-assets()`                | Total number of minted assets.                   |

---

## 🔐 Constants & Limits

| Constant              | Value   | Purpose                           |
| --------------------- | ------- | --------------------------------- |
| `max-level`           | `100`   | Max level a player can reach.     |
| `max-experience`      | `10000` | Max XP a player can have.         |
| `max-metadata-length` | `256`   | Max metadata URI string length.   |
| `max-batch-size`      | `10`    | Max items in batch mint/transfer. |

---

## 🚫 Error Codes

| Code   | Description                                    |
| ------ | ---------------------------------------------- |
| `u100` | Unauthorized access (owner only).              |
| `u101` | Asset not found.                               |
| `u102` | Not authorized to perform action.              |
| `u103` | Invalid input (e.g., empty list, bad lengths). |
| `u104` | Invalid price (must be > 0).                   |

---

## ⚙️ Setup & Deployment

### Prerequisites

* Clarity-compatible development environment (e.g., [Clarinet](https://github.com/hirosystems/clarinet)).
* STX wallet for deploying and interacting with contract.

### Steps

1. Clone this repository.
2. Open with Clarinet or your preferred Clarity IDE.
3. Deploy using:

```bash
clarinet deploy
```

4. Use Clarinet console or frontend interface to interact with functions.

---

## 💡 Example Usage

### Mint a Single Asset

```clojure
(mint-asset "ipfs://Qm123...xyz" true)
```

### Batch Mint

```clojure
(batch-mint-assets
  (list "uri1" "uri2" "uri3")
  (list true true false))
```

### Transfer

```clojure
(transfer-asset u1 'ST3...ABC')
```

### List for Sale

```clojure
(list-asset-for-sale u1 u500)
```

### Purchase

```clojure
(purchase-asset u1)
```

### Update Player Stats

```clojure
(update-player-stats u2500 u15)
```

---
