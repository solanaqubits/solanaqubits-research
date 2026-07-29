# Source Links — Jito Restaking and NCNs

Status checked: 2026-07-29

Companion source list for:

- `articles/jito-restaking-ncn-landscape.md`
- Website article: https://solanaqubits.com/research/jito-restaking-ncn-landscape

This source index follows the website article's evidence hierarchy. Official documentation and the Apache-2.0 program repository are primary for structural claims. The official interface is the only source used for entity names, status labels, and published totals. Onchain measurements were taken independently through a public RPC endpoint and are reported alongside official figures rather than replacing them.

## Primary protocol documentation

- Jito (Re)staking overview
  https://www.jito.network/docs/restaking/jito-restaking-overview/
  First-party protocol overview. Primary source for the three-participant model, the mutual opt-in handshake and the wording that operators "must be accepted", the warm-up period of one full epoch excluding the current partial epoch, the NCN-defined withdrawal cooldown, the lifecycle phases, the program addresses and versions, and the explicit statement that the slashing program is not currently live.

- Jito Omnidocs — restaking sources
  https://github.com/jito-foundation/jito-omnidocs/tree/master/restaking
  Markdown source files behind the published documentation. Used for core concepts, account descriptions, CLI references, and the NCN implementation overview. Primary source for the detail that the NCN initializes the `NcnOperatorState` account and that both parties subsequently warm up and cool down their own side.

- Jito Restaking repository
  https://github.com/jito-foundation/restaking
  Apache-2.0 program source. Primary source for the generated client account structs used to derive account sizes and field offsets, the published TypeScript SDK references, and the security audit directory.

- Security audits directory
  https://github.com/jito-foundation/restaking/tree/master/security_audits
  Published audit reports from Ottersec, Certora (two reports), and Offside, dated across late 2024. Used for the audit statement only; audit coverage is point-in-time review of the reviewed code, not a safety guarantee, and does not extend to individual NCN programs.

## Official interface and published figures

Interface pages are dynamic. They are the correct source for entity names and status labels, and the only source for the published totals reproduced in the article, but every value requires live re-verification before reuse.

- Jito (Re)staking
  https://www.jito.network/restaking/
  Official restaking interface. Source for the listed vaults, VRT names, reported per-vault TVL, and the operators shown against each vault.

- Node consensus networks directory
  https://www.jito.network/restaking/ncns/
  Official NCN directory. Source for NCN names, categories, the Operational and Coming Soon labels, and the onchain addresses published for TipRouter, Switchboard, and DePHY.

- Node operators directory
  https://www.jito.network/restaking/node-operators/
  Official operator directory. Source for operator names, vaults connected, delegation counts, join dates, and the onchain addresses published for the connected operators.

- Ecosystem stats
  https://www.jito.network/restaking/stats/
  Official totals for TVL in USD, depositor count, percentage of JitoSOL restaked, and the vault, operator, and NCN counts including the "Jito Whitelisted" split used in the comparison table.

## Reference implementations

- Jito Tip Router
  https://github.com/jito-foundation/jito-tip-router
  Reference NCN implementation covering MEV tip distribution, including an operator client and a permissionless keeper. Used as the concrete example of what an NCN workload involves.

- Restaking TypeScript SDK
  https://www.npmjs.com/package/@jito-foundation/restaking-sdk
  Published client library for the restaking program.

- Vault TypeScript SDK
  https://www.npmjs.com/package/@jito-foundation/vault-sdk
  Published client library for the vault program.

## Onchain measurement method

Counts in the article were measured directly rather than taken from any dashboard. The method is reproducible from a public RPC endpoint without an API key, indexer, or paid data provider.

- Solana mainnet public RPC
  https://api.mainnet-beta.solana.com
  Endpoint used for `getProgramAccounts` queries against both programs, and for `getSlot` to record the measurement point. Public endpoints rate-limit or disable `getProgramAccounts` inconsistently.

Account sizes were computed from the generated client structs in the restaking repository and used as `dataSize` filters:

| Account | Size | Program |
|---|---|---|
| `Ncn` | 592 bytes | Restaking |
| `Operator` | 520 bytes | Restaking |
| `NcnOperatorState` | 440 bytes | Restaking |
| `Vault` | 1111 bytes | Vault |

Relationship state was read from the two `SlotToggle` fields in `NcnOperatorState`. A side counts as opted in when its `slot_added` exceeds its `slot_removed`; a relationship is mutually active only when this holds for both sides.

## Use notes

- Keep the restaking program described as a registry that holds no funds, and the vault program as the component holding tokenized stake. Do not merge them into a single "restaking protocol" claim about where value sits.
- Keep the detail that the NCN initializes the NCN-to-operator relationship account. It is the difference between "an operator applies" and "an operator cannot apply until an NCN opens a record".
- Keep vault receipt tokens (kySOL, kyJTO, fragSOL, fragJTO, ezSOL, ezJTO, bzSOL, rstSOL, dmSOL, LovePIPE) classified as vaults, never as NCNs.
- Report the operator-count difference between the onchain registry and the official interface rather than reconciling it. The official total matches its own whitelist.
- Do not name the nine registered NCN accounts that no first-party source names. Address patterns are not evidence of ownership.
- Treat the slashing status as a dated fact and re-check it; the risk framing inverts once the program ships.
- Do not derive per-token totals from reported USD TVL without confirming token decimals for each underlying mint.
- Do not publish acceptance probabilities, eligibility assessments, or operator revenue estimates from these sources; none of them support such claims.
- Re-derive account sizes from the current structs before reusing the `dataSize` filters; layouts change between program versions.
- Listing a program, repository, interface page, network, vault, or operator does not imply endorsement, partnership, official approval, eligibility, acceptance, stake, delegation, APY, earnings, or guaranteed outcomes.
