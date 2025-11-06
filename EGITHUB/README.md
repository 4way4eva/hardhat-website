# EGITHUB - Mega Zion Bundle Minting Infrastructure

This directory contains the token schema, sample metadata, watchtower data, and minting infrastructure for the first Mega Zion bundle deployment.

## Directory Structure

```
EGITHUB/
├── mint/
│   ├── schema/
│   │   └── EVOL.ENFT.v1.rain.json          # Token schema with Rain/Blessing extension
│   ├── metadata/
│   │   ├── bleu_jewel_0001.json            # RARELY 1if1 sample metadata
│   │   ├── plasmarain_P2025_01.json        # PlasmaRain sample metadata
│   │   └── spacebar_SB77.json              # SpaceBar Coin sample metadata
│   ├── calldata/
│   │   └── mint_RA_calldata.txt            # Ethers.js calldata example
│   └── multisig/
│       └── multisig_tx_RA.json             # Multisig transaction template
└── watchtower/
    └── watchtower.csv                       # Watchtower tracking data
```

## Token Schema (EVOL.ENFT.v1)

The token schema extends the standard NFT metadata format with Rain/Blessing-specific fields:

- **mint_node**: Planetary/Orbital node (e.g., Saturn, Pluto, Enato)
- **ritual_window**: ISO timestamp or Tachometer tag for φ-Boost
- **broadcast_id**: DREAMKAM/EVOLSTUDIOS stream ID
- **rarity_index**: Value between 0 and 1
- **non_transferable**: Boolean flag for lineage anchors
- **lineage_signatures**: Array of role-based signatures
- **provenance_sha3_256**: SHA3-256 hash for provenance verification
- **watchtower_row_id**: Reference to watchtower tracking system

## Sample Metadata

### 1. BLEU Jewel RARELY 1if1 #0001
- **Type**: Single ceremonial jewel
- **Mint Node**: Saturn Ring-Bar
- **Rarity**: 1.0 (Mythic)
- **Transferable**: No (lineage anchor)
- **Special**: Flame Crown refinement, φ-Boost ceremony

### 2. PlasmaRain Festival ENFT #P-2025-01
- **Type**: HoloConcert broadcast NFT
- **Mint Node**: Enato
- **Rarity**: 0.94
- **Transferable**: Yes
- **Special**: Variable yield linked to live participation

### 3. SpaceBar Coin SB-77
- **Type**: Orbital remine/refine credit
- **Mint Node**: BLEUFleet-Orbit-7
- **Rarity**: 0.82
- **Transferable**: Yes
- **Special**: Redeemable for remine jobs and refinery access

## Watchtower CSV

The watchtower CSV tracks all minted tokens with the following columns:

- contract
- token_id
- name
- owner
- metadata_ipfs_cid
- image_ipfs_cid
- provenance_sha3_256
- enft_schema
- treasury_anchor (BLEULIONTREASURY™)
- non_transferable
- issued_date
- notes

## Minting Process

### 1. Generate Calldata

Use the example in `mint/calldata/mint_RA_calldata.txt`:

```javascript
const { ethers } = require("ethers");
const iface = new ethers.utils.Interface(["function mint(address to,uint256 tokenId,string memory tokenURI)"]);
const calldata = iface.encodeFunctionData("mint", [
  "0x638f2c25DC4346dbEF5566a2D5DA871F6D268b8a", // recipient
  999901, // tokenId
  "ipfs://PLACEHOLDER_METADATA_CID_R1"
]);
console.log("calldata:", calldata);
```

### 2. Create Multisig Transaction

Use the template in `mint/multisig/multisig_tx_RA.json`:

1. Replace `0xPLACEHOLDER_CALLDATA` with the generated calldata
2. Set the correct nonce for your Gnosis Safe
3. Submit the transaction for approval

### 3. Update Watchtower

After minting, append a new row to `watchtower/watchtower.csv` with the actual IPFS CIDs and transaction details.

## Next Steps

Choose one of the following actions:

1. **Generate IPFS-ready metadata files** with real CIDs
2. **Produce ritual PDF** (BLEU_SEAL) for RARELY_1if1 and broadcast manifest
3. **Create batch mint script** that reads watchtower.csv and proposes multisig txs
4. **Simulate PlasmaRain stream mint** with pipeline steps and expected yield

## Contract Address

All samples reference contract: `0x918144e4916eB656Db48F38329D72517a810f702`

## Treasury

All tokens are anchored to: **BLEULIONTREASURY™**
