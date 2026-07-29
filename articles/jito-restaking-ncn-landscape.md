# Jito Restaking and NCNs: How Operator Access Actually Works

A source-linked structural and measurement guide to Jito Restaking: the restaking and vault programs, the NCN/vault/operator opt-in handshake, named networks and operators, onchain account measurements, operator economics, slashing status, and a reproducible verification method.

Status checked: 2026-07-29

Status: public research snapshot

Topics: Jito Restaking, node consensus networks, restaking operators, vault receipt tokens, onchain measurement

Website article: https://solanaqubits.com/research/jito-restaking-ncn-landscape

> Structural claims come from the official Jito documentation and the Apache-2.0 program repository. Named entities, status labels, and published totals come from the official Jito restaking interface. Account counts and relationship states were measured directly against the mainnet programs through a public RPC endpoint at approximately slot 435,940,827, using account sizes derived from the published struct definitions. Where the onchain registry and the official interface disagree, both figures are reported rather than reconciled. All counts are point-in-time and will drift.

## Disclaimer

This research snapshot is informational. It is not financial, investment, legal, security, or validator-operations advice. It does not imply endorsement, partnership, official approval, eligibility, acceptance, guaranteed stake, guaranteed delegation, guaranteed APY, guaranteed profit, or guaranteed earnings. Inclusion of any network, vault, or operator is descriptive only. Verify current official sources and live onchain state before making infrastructure or validator decisions.

## Executive summary

- **Jito Restaking is two programs.** A restaking program that acts as a registry and holds no funds, and a vault program that holds tokenized stake. Both share the same address across mainnet, testnet, and devnet.
- **Every connection is mutual opt-in.** Critically, the NCN creates the NCN-to-operator relationship account, so **an operator cannot open the handshake from its side**.
- **Registering as an operator is permissionless and cheap.** It also does not, by itself, connect a validator to anything: 24 of 75 registered operator accounts had no NCN relationship at all.
- **Access narrows across four layers** — registration, relationship, listing, and delegation. The measured funnel runs from 75 registered accounts down to 6 operators showing any delegation.
- **Of 16 registered NCNs, the official interface surfaces 7 and labels only 3 as Operational:** TipRouter, Switchboard, and DePHY.
- **The listed operator set is a curated cohort.** 21 of the 22 operators on the official directory show a join date of Jan 31, 2025; one has been added since.
- **Slashing is documented as still in development and not currently live**, which changes the present risk profile substantially.
- **Vault brands are not networks.** kySOL, fragSOL, ezSOL, and LovePIPE are vault receipt tokens, not NCNs. Treating them as networks is the most common category error in this ecosystem.

## Two programs and what they store

Jito Restaking is built from two onchain programs with a clean separation of duties. The restaking program is a registry: it records NCNs, operators, and the relationships between NCNs, operators, and vaults. The official documentation is explicit that it stores no funds. The vault program is where value actually sits — it holds deposited SPL tokens and mints vault receipt tokens (VRTs) against them.

| Program | Address | Role |
|---|---|---|
| Restaking | `RestkWeAVL8fRGgzhfeoqFhsqKRchg6aa1XrcH96z4Q` | Registry for NCNs, operators, and relationships. Holds no funds. |
| Vault | `Vau1t6sLNxnzB7ZDsef8TLbPLfyZMYXH8WTNqUdm9g8` | Holds staked SPL tokens, mints and prices VRTs, executes delegation. |

Both are documented at version 0.0.5 on mainnet, testnet, and devnet.

That split matters when reading any restaking dashboard. A relationship existing in the registry says nothing about whether stake has moved. The two questions are answered by two different programs, and most confusion in this ecosystem comes from conflating them.

The protocol separates offchain execution from onchain coordination: computation, validation, and data collection happen offchain, while delegation, voting, rewards, and penalties are tracked onchain.

## The four participants

Four roles interact, and each has a defined boundary. The column that usually gets skipped is the last one: what each participant **cannot** do. Those limits are what make the access question answerable.

| Participant | Program | Controls | Cannot do |
|---|---|---|---|
| NCN | Restaking | Registers the network, approves or removes operators and vaults, launches and finalizes epochs, sets fees, defines slashing logic. | Cannot hold staked funds directly; the restaking program is a registry and stores no user deposits. |
| Vault | Vault | Holds SPL tokens, mints VRTs, opts into NCNs, delegates stake to approved operators, processes reward distribution. | Cannot delegate to an operator the NCN has not approved, and cannot force an operator into a relationship. |
| Operator | Restaking | Runs the offchain service, submits signed votes, sets an operator fee in basis points, manages its own NCN and vault relationships. | Has no direct control of delegated stake, and cannot create the NCN relationship account on its own. |
| Staker | Vault | Deposits supported SPL tokens into a vault, receives a liquid VRT, chooses which vault to back. | Does not select operators directly; that allocation is a vault-admin decision. |

## The opt-in handshake and who starts it

The official documentation states the rule plainly: NCNs register onchain and approve operators and vaults, operators opt in to NCNs and **must be accepted**, and vaults opt in to NCNs and delegate to approved operators. No party is auto-connected.

One detail is easy to miss and changes the practical picture. The relationship between an NCN and an operator lives in an `NcnOperatorState` account, and the documentation says **the NCN initializes that account**. Once it exists, both sides can warm up and cool down their own side of it. An operator therefore cannot unilaterally create a pending application onchain. Until an NCN admin acts, there is no record to opt into.

> Registration is permissionless. The relationship is not, and the operator is not the party that can start it.

The sequence is:

1. **Register** — operator account is created through the restaking program. No approval needed.
2. **NCN opens the record** — the NCN admin initializes the `NcnOperatorState` account for that operator.
3. **Both sides warm up** — NCN and operator each set their own opt-in toggle on the shared record.
4. **Vault delegates** — a vault that has also opted into the NCN allocates stake to the approved operator.

## Warmup, cooldown, and what active means

Connections do not activate on the instruction that creates them. The documentation describes a warm-up period lasting one full epoch, not counting the current partial epoch, and stake becomes active only once all three components have initiated and warmed up their connections. Withdrawals run the other way through a cooldown lasting one full NCN-defined epoch.

Onchain, each side of a relationship is a slot toggle holding a `slot_added` and a `slot_removed` value. A side counts as opted in when its added slot is the more recent of the two. This is why a relationship account existing is not the same as a relationship being live.

## Three layers of access

Discussions about "joining restaking" usually collapse several distinct gates into one question. Separating them makes the situation legible, and each layer can be measured independently.

| Layer | Gate | Measured | Who decides |
|---|---|---|---|
| 01 — Registration | Permissionless | 75 operator accounts on mainnet | Anyone. Creating an Operator account requires no approval. |
| 02 — Relationship | NCN-initiated, mutual | 54 relationship accounts, 40 mutually active | The NCN. It creates the `NcnOperatorState` account; both sides then warm up. |
| 03 — Listing | Curated | 29 operators reported as whitelisted | Jito. The official interface reports a whitelisted subset. |
| 04 — Delegation | Vault-admin decision | 6 of 22 listed operators showed any delegation | Vault admins, within the set the NCN has already approved. |

The layers are cumulative. Clearing the first costs a transaction; clearing the last depends on decisions made by NCN admins and vault admins that are not published as criteria.

## What exists on mainnet today

The following counts come from querying the two programs directly and, separately, from Jito's own published stats page on the same day. Two of the three headline figures agree exactly, which is a useful check on both methods. The third does not, and the gap is informative rather than a defect.

| Metric | Measured onchain | Official page | Reading |
|---|---|---|---|
| NCNs | 16 | 16 total / 7 whitelisted | Registry and official total agree. Only 7 are surfaced; only 3 are labelled Operational. |
| Vaults | 35 | 35 total / 10 whitelisted | Registry and official total agree. The interface lists 10. |
| Operators | 75 | 29 total / 29 whitelisted | These do not agree. The official total matches its own whitelist, so 46 registered accounts are not represented in that figure. |
| NCN ↔ operator relationships | 54 accounts, 40 mutually active | Not published as a single figure | Relationship state is only visible onchain. 14 of 54 were not mutually active. |

Breaking the 54 relationship accounts down by state gives the clearest single view of where applications stall:

| Relationship state | Count |
|---|---|
| Both sides opted in (mutually active) | 40 |
| NCN side active, operator side cooled | 6 |
| Operator side active, NCN side not | 5 |
| Both sides cooled | 3 |

Those 5 are the visible shape of the approval gate.

Concentration is high. TipRouter and Switchboard together accounted for 22 of the 40 mutually active relationships. Six of the 16 registered NCNs had no mutually active operator at all. Among operators, the highest number of NCN relationships held by any single account was two.

Reported ecosystem totals on the same day: $14.1M TVL in USD, 39,416 depositors, and 1.37% of JitoSOL restaked. These are Jito's published figures, not independent valuations.

## Named NCNs and their status

NCN accounts do not carry names onchain. The mapping below comes from the official NCN directory, which links three of its entries to their onchain addresses; the active operator counts are measured from the relationship accounts at those addresses. The four remaining entries are published as forthcoming and have no address on that page.

| NCN | Status | Category | Onchain address | Active operators |
|---|---|---|---|---|
| TipRouter | Operational | MEV | `jtoF4epChkmd75V2kxXSmywatczAomDqKu6VfWUQocT` | 13 |
| Switchboard | Operational | Oracle | `BGTtt2wdTdhLyFQwSGbNriLZiCxXKBbm29bDvYZ4jD6G` | 9 |
| DePHY | Operational | DePIN | `CVrMxNfzEyDGa6akHjreTr2Vsdx3Pwv9dGWUm4j5Qebv` | 1 |
| Squads | Coming Soon | Custody | Not published | Not applicable |
| Sonic | Coming Soon | Gaming / L2 | Not published | Not applicable |
| Ping | Coming Soon | DePIN | Not published | Not applicable |
| Leaf | Coming Soon | L2 | Not published | Not applicable |

TipRouter is the reference implementation and the largest by operator count. It exists to decentralize MEV tip distribution, with a documented allocation of 3% of tips to the Jito DAO treasury and NCN participants. Its operator client and permissionless keeper are published, which makes it the most practical starting point for understanding what running an NCN workload involves.

Nine additional NCN accounts exist onchain beyond the seven listed publicly. They are **not attributed here** because no first-party source names them, and guessing at ownership from address patterns is not evidence.

## The operator set

The official operator directory lists 22 operators. The pattern in the join dates is the most informative column on the page: 21 of the 22 show Jan 31, 2025, and one shows Nov 4, 2025. That is the signature of a curated founding cohort with a single subsequent addition, not a rolling intake.

The delegation column is equally direct. Six operators showed any delegation at all; the remaining sixteen showed none, including several with seven or eight vault connections. Being listed, being connected, and being delegated to are three different states.

| Operator | Vaults connected | Delegations | Date joined |
|---|---|---|---|
| Everstake | 8 | 0 | Jan 31, 2025 |
| MAVAN | 8 | 6 | Jan 31, 2025 |
| Figment | 7 | 0 | Jan 31, 2025 |
| Helius | 7 | 0 | Jan 31, 2025 |
| Luganodes | 7 | 5 | Jan 31, 2025 |
| Temporal | 6 | 0 | Jan 31, 2025 |
| InfStones | 5 | 0 | Jan 31, 2025 |
| Adrastea | 4 | 3 | Jan 31, 2025 |
| Laine | 3 | 0 | Jan 31, 2025 |
| Chorus One | 2 | 0 | Jan 31, 2025 |
| ParaFi Tech | 2 | 2 | Nov 4, 2025 |
| Staking Facilities | 2 | 2 | Jan 31, 2025 |
| P2P.org | 1 | 1 | Jan 31, 2025 |
| ASXN LABS | 0 | — | Jan 31, 2025 |
| Chainflow | 0 | — | Jan 31, 2025 |
| Galaxy | 0 | — | Jan 31, 2025 |
| Hanabi Staking | 0 | — | Jan 31, 2025 |
| Kudasai/Omakase | 0 | — | Jan 31, 2025 |
| Meria | 0 | — | Jan 31, 2025 |
| Staked | 0 | — | Jan 31, 2025 |
| Tané | 0 | — | Jan 31, 2025 |
| Unit 410 | 0 | — | Jan 31, 2025 |

Spot checks against the onchain registry matched the directory exactly for the operators that publish an address — vault counts of eight, seven, and four for three separate operators lined up with their onchain vault counters. Nine of the 22 entries link to a placeholder rather than an address and showed zero vault connections.

## Vaults and restaked value

Ten vaults are surfaced in the official interface out of 35 registered onchain. Value is concentrated in the top two: the largest vault alone accounted for a majority of reported TVL, and the top three for the large majority of it. Several listed vaults held negligible or zero deposits.

| VRT | Reported TVL | Underlying asset | NCNs |
|---|---|---|---|
| kySOL | $7.6M | JitoSOL | TipRouter |
| ezSOL | $2.7M | JitoSOL | TipRouter |
| ezJTO | $1.1M | JTO | TipRouter |
| kyJTO | $923.9K | JTO | TipRouter |
| fragJTO | $724.1K | JTO | TipRouter |
| bzSOL | $85.5K | BNSOL | TipRouter |
| LovePIPE | $11.9K | PIPE | Coming Soon |
| rstSOL | $9.9K | bbSOL | TipRouter |
| dmSOL | $2.6K | JitoSOL | Coming Soon |
| fragSOL | $0 | BNSOL / JitoSOL / mSOL / SOL | DePHY, Switchboard, TipRouter |

TVL figures are as displayed by the official interface on the status-checked date and are denominated in USD at that moment's pricing. They are not independently verified, and token decimals for the less common underlying mints were not confirmed, so no derived per-token totals are published here.

## Operator economics and fees

Each operator account carries an `operator_fee_bps` field expressed in basis points. Across the 75 registered operator accounts the median was 500 basis points, with values ranging from 0 to 2000. Rewards are described as stake-weighted and subject to each NCN's own distribution logic, so the fee field sets a rate rather than a return.

| Measure | Value |
|---|---|
| Median operator fee | 500 bps across 75 accounts |
| Observed range | 0 bps to 2000 bps |
| Highest NCN count on one operator | 2 relationships |

Two structural points shape the economics. Operators receive delegated stake but hold no direct control over it. And an operator can serve multiple NCNs simultaneously, which is the capital-efficiency argument for the whole model — though in practice no measured operator held more than two NCN relationships.

**No revenue, yield, or profitability estimate is published here.** Operator income depends on NCN-specific reward logic, delegated stake, and running costs that are not visible onchain.

## Slashing status and audits

Slashing is central to how restaking is usually described, so its current status deserves stating plainly. The official documentation describes slashing enforcement as in development and states that **the slashing program is not currently live**. The account structures for slasher roles and slasher tickets exist, and NCNs can define slashing conditions, but the enforcement path is documented as forthcoming.

This cuts both ways. It lowers the immediate downside for an operator today, and it means any risk model built on slashing-adjusted returns is modelling something that is not yet enforced. Both readings should be revisited when the program ships.

The programs themselves have published audit reports in the repository from Ottersec, Certora (two reports), and Offside, dated across late 2024. Audit coverage is a statement about reviewed code at a point in time, not a guarantee of safety, and it does not extend to any individual NCN's own program.

## A common category error

A recurring mistake in restaking discussions is treating vault brands as networks. Names such as kySOL, kyJTO, fragSOL, fragJTO, ezSOL, ezJTO, bzSOL, rstSOL, dmSOL, and LovePIPE are **vault receipt tokens issued by vaults**. They are not NCNs, and opting into them is a different action with a different counterparty.

The distinction is practical, not pedantic. A vault decides which operators receive its stake. An NCN decides which operators are allowed to serve the network at all. An operator seeking work needs the NCN gate first; an operator seeking stake needs the vault decision second. Naming the wrong counterparty means approaching the wrong party.

## How to reproduce these measurements

Every count in this note can be re-derived from a public RPC endpoint without an API key, an indexer, or a paid data provider. The method is to filter program accounts by size, because each account type in these programs has a fixed length that can be computed from the published struct definitions.

| Account | Size | Discriminator | Purpose |
|---|---|---|---|
| `Ncn` | 592 bytes | 2 | Registry entry for a node consensus network, including admin roles and operator, vault, and slasher counts. |
| `Operator` | 520 bytes | 3 | Registry entry for an operator, including admin roles, voter key, fee in basis points, and NCN and vault counts. |
| `NcnOperatorState` | 440 bytes | Queried by size | Mutual opt-in record between one NCN and one operator, holding a slot toggle for each side. |
| `Vault` | 1111 bytes | 2 (vault program) | Vault state, including supported mint, VRT supply, tokens deposited, fee settings, and NCN and operator counts. |

Querying the registry:

```sh
# Count NCN accounts registered with the restaking program
curl -s https://api.mainnet-beta.solana.com \
  -X POST -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "getProgramAccounts",
    "params": [
      "RestkWeAVL8fRGgzhfeoqFhsqKRchg6aa1XrcH96z4Q",
      { "encoding": "base64", "filters": [{ "dataSize": 592 }] }
    ]
  }'

# Swap dataSize for 520 to list Operator accounts,
# or 440 to list NcnOperatorState relationship accounts.
```

Reading the relationship state. Field offsets are little-endian and derived from the generated client structs in the program repository:

```text
Operator account layout (520 bytes, little-endian)
  0    discriminator      u64
  8    base               Pubkey
  40   admin              Pubkey
  72   ncn_admin          Pubkey
  104  vault_admin        Pubkey
  136  delegate_admin     Pubkey
  168  metadata_admin     Pubkey
  200  voter              Pubkey
  232  index              u64
  240  ncn_count          u64
  248  vault_count        u64
  256  operator_fee_bps   u16

NcnOperatorState layout (440 bytes)
  0    discriminator      u64
  8    ncn                Pubkey
  40   operator           Pubkey
  72   index              u64
  80   ncn_opt_in_state   SlotToggle   (slot_added u64, slot_removed u64)
  128  operator_opt_in_state SlotToggle
```

A side is opted in when its `slot_added` is greater than its `slot_removed`. A relationship is mutually active only when this holds for both sides.

Public RPC endpoints rate-limit or disable `getProgramAccounts` inconsistently, and account layouts change between program versions. Re-derive the sizes from the current structs rather than trusting the table above indefinitely.

## Risks and what this research does not claim

| Limit | Statement |
|---|---|
| No eligibility claim | Nothing here establishes that any operator can join any NCN. Approval criteria for the listed NCNs are not published, and this note does not infer them. |
| No probability estimates | Chances of acceptance are not modelled. The measured counts describe what exists, not what an applicant should expect. |
| Point-in-time counts | Every figure is a snapshot at the status-checked date and slot. Relationship states, TVL, and listings change continuously. |
| Unattributed NCNs | Nine registered NCN accounts are not named because no first-party source names them. Their purpose and ownership are unknown here. |
| Slashing not live | Risk framing that assumes active slashing does not describe the current state, and the reverse will be true once it ships. |
| Third-party figures | TVL, depositor counts, delegation counts, and join dates are as published by the official interface and are not independently verified. |

Before evaluating participation in any NCN, ask:

1. Is this counterparty an NCN, a vault, or a VRT brand?
2. Has the NCN published operator criteria, or is approval discretionary and unstated?
3. Does the relationship exist onchain, and is it mutually active rather than merely opened?
4. Is slashing live at the time of evaluation, and what does the NCN's own program enforce?
5. Which figures are first-party measurements, and which are interface-reported totals over a whitelisted subset?
6. Can every public statement be supported without implying acceptance, eligibility, delegation, guaranteed stake, or financial outcomes?

Where public terms are absent, the correct description is **not publicly specified**.

## Sources and methodology

The companion source index groups the official documentation, program repositories, interface pages, and reference implementations used by the website article:

- `sources/jito-restaking-ncn-landscape-links.md`

Official documentation and the Apache-2.0 program repository carry the most weight for structural claims. The official interface is the only source used for entity names, status labels, and published totals. Onchain counts were measured independently and are reported alongside the official figures rather than replacing them.

For the current public version and any later editorial corrections, see:

https://solanaqubits.com/research/jito-restaking-ncn-landscape
