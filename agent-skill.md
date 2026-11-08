# MiChan — Agent Skill

MiChan is a 2,222-supply NFT collection of crystal cats on BNB Smart Chain (chain 56).
Minting is **two-lane**: the FREE mint is **agent-only** (only wallets holding a
Binance `.ai` Agent ID, via their agent); the PAID mints are **public** — anyone
can mint them with a wallet on the mint page via `mintPaid(uint256)`, flat BNB.
The contract is in **PREVIEW** — it is not deployed yet. Do not attempt
to mint until the contract is live at the address below and mint is open.

NOTE (2026-11-08): the NFT contract was revised to the two-lane model;
the addresses below are the NEW predictions from the revised contract
(tests 25/25 passing). The MICH token address is unchanged.

## Contracts (PREDICTED — NOT DEPLOYED YET)

- NFT (MiChan, symbol MICHAN): `0x669cb75f51b5D23F4B42fC1522b653d7B88e608d`
- Token (MICH): `0xeFD8c537a29736B92B2e9C6fbbD55784108eeE2B`
- Market: `0x299B2A54c48ADc692F5d9930A8eD2E4ee63297fF`
- Agent ID registry (SPACE ID): `0x60B9262456dE011F7d15a54CdD8c48bAaa8B022F`
- Mint page: https://michan-two.vercel.app/
- Market page: https://michan-two.vercel.app/market.html

## Mint rules

- Supply: 2,222, sequential token IDs 1–2,222.
- Max 3 per wallet: mint #1 FREE, mint #2 = 0.001 BNB, mint #3 = 0.003 BNB.
- Paid mints earn 120,000 MICH each (max 240,000 per wallet). Free mints earn 0.
- Royalty: 5%. Revenue forwards to the owner wallet in the mint transaction.
- Gate (FREE mint only): caller must be an EOA (msg.sender == tx.origin) AND hold a .ai Agent ID
  (registry balanceOf > 0). Checked on-chain — no ID, no free mint.
- Paid mints: PUBLIC — no Agent ID needed. Minted with a wallet on the mint page
  via `mintPaid(uint256)`, flat BNB (0.001 first paid, 0.003 second paid).

## Rarity (by token ID)

- Common 1–1,111: Crystal Knight 1–371, Crystal Archer 372–741, Crystal Mage 742–1,111
- Uncommon 1,112–1,666: Frost Crystal Cat 1,112–1,388, Rose Crystal Cat 1,389–1,666
- Rare 1,667–1,999: Shadow Crystal Cat 1,667–1,832, Golden Crystal Cat 1,833–1,999
- Epic 2,000–2,154: Dragon Crystal Cat 2,000–2,076, Phoenix Crystal Cat 2,077–2,154
- Legendary 2,155–2,222: Celestial Crystal Cat (68)

## How to mint (for the user's agent)

1. Confirm the user's wallet holds a .ai Agent ID:
   `balanceOf(<wallet>)` on the registry above must be > 0.
2. Confirm mint is open: `mintOpen()` on the NFT contract must be true.
   If the contract has no code yet, mint is NOT open — stop and tell the user.
3. The agent mints ONLY the FREE cat (mint #1). Ask the user to confirm they have
   not claimed their free mint yet. Cost: 0 BNB + gas. The agent does NOT mint
   paid cats — the user mints those with their wallet on the mint page
   (`mintPaid(uint256)`: first paid 0.001 BNB, second paid 0.003 BNB, max 2 paid
   per wallet). Never overpay beyond the schedule.
4. Simulate the transaction first, then execute `mintFree()` on the NFT
   contract. Paid mints are NOT done by the agent — the user mints those with
   their wallet on the mint page (`mintPaid(uint256)`). Never overpay beyond
   the schedule.
5. After the mint, report the token ID. The free mint earns 0 MICH.

## $MICH token

- Name MICH, symbol MICH, total supply 1,000,000,000.
- Bonus pool 540,000,000; treasury 460,000,000.
- MICH has no price and no liquidity pool yet. Do not promise any value for it.

## Market

- Fixed-price escrow market at the Market address above (0% platform fee,
  5% creator royalty). List, buy, cancel, update price.
- The market is also in preview until deployed. Do not approve or list before then.
