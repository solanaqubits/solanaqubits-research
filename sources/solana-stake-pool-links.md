# Solana Stake Pool Links

Source links referenced by `articles/solana-stake-pool-delegation-landscape.md`.

Last updated: 2026-06-21

Editorially updated: 2026-07-29

Scoped rkuSOL monitoring update: 2026-08-15

## Discussion

A short launch and discussion thread for this resource is available on X:

https://x.com/solanaqubits/status/2067259338364711235

## Stake pool and delegation program links

- Phase
  - <https://phase.cc/apply>
  - <https://phase.cc/delegation>
- JPool
  - <https://docs.jpool.one/delegation-strategy/how-to-join-jpool-delegation-program.html>
  - <https://docs.jpool.one/delegation-strategy/inclusion-and-removal-criteria.html>
- BlazeStake
  - <https://stake-docs.solblaze.org/protocol/delegation-strategy>
- DynoSol
  - <https://docs.dynosol.io/>
  - <https://www.dynosol.io/#stats>
- DoubleZero
  - <https://doublezero.xyz/dzdp>
- Definity
  - <https://definity.finance/whitelist-apply>
- JagPool
  - <https://docs.jagpool.xyz/DELEGATION-STRATEGY/Delegation-Criteria>
  - <https://docs.jagpool.xyz/DELEGATION-STRATEGY/Validator-Application-Process>
- Edgevana
  - <https://stake.edgevana.com/validators>
  - <https://stake.edgevana.com/docs/validators/eligibility>
  - <https://stake.edgevana.com/docs/validators/delegation-strategy-algorithm>
  - <https://nodes.edgevana.com/launch>
- SolStrategies
  - <https://support.solstrategies.io/stke-stake-pool/delegation-strategy>
- Vault
  - <https://docs.thevault.finance/delegation/validator-application-process>
- Marinade
  - <https://docs.marinade.finance/marinade-protocol/protocol-overview/stake-auction-market/eligibility-criteria>
- Jito
  - <https://www.jito.network/docs/jitosol/jitosol-liquid-staking/stake-pool-operations/delegation-criteria/>
  - <https://forum.jito.network/t/jip-28-accelerate-bam-adoption/904>
- Shinobi xSHIN
  - <https://xshin.fi/#Strategy>

The canonical website registry remains 15 actionable programs. rkuSOL is intentionally excluded from that count and indexed separately below because no working public validator-admission route was verified.

## rkuSOL / Raiku monitoring-only sources

Snapshot checked on finalized mainnet data at slot `439,419,080` in epoch `1017` on 2026-08-15. The validator list contained one active vote account with `187,167.943 SOL`, zero transient stake, and 100% of delegated validator stake; pool-state accounting was `187,168.173 SOL`, rounded to `~187.2k SOL`. Sanctum's interface displayed about `187,253.88 SOL` during review, so UI TVL and finalized on-chain accounting must remain separately attributed.

### Official Raiku and Sanctum sources

- Raiku website: <https://www.raiku.com/>
- Raiku X / Twitter: <https://x.com/raikucom>
- rkuSOL documentation: <https://docs.raiku.com/staking/rkusol>
- Staking fee FAQ: <https://docs.raiku.com/staking/staking-faqs> — conflicts with the finalized pool state on withdrawal fees; verify live before quoting costs
- Validator quickstart: <https://docs.raiku.com/validator-quickstart> — describes pilot-partner client access; it is not a public rkuSOL application or allocation guarantee
- Published apply page: <https://docs.raiku.com/apply-1> — its linked validator form returned HTTP 404 when checked on 2026-08-15
- Published validator form: <https://forms.raiku.com/earn_with_raiku> — unavailable with HTTP 404 on the checked date; retain only as a dated record, not an active Apply route
- Contact page: <https://raiku.com/contact-us> — general inquiry channel only; it does not establish application, acceptance, stake, timing, or a response SLA
- Sanctum rkuSOL app: <https://app.sanctum.so/stake/rkuSOL> — live UI metrics may be dynamic or cached
- Sanctum launch article: <https://sanctum.so/blog/raiku-launches-rkusol-lst-with-sanctum>
- Raiku launch article: <https://raiku.com/blog/rkusol-a-third-yield-source-enters-the-solana-lst-stack> — the six external validator partners were a historical committed pipeline statement, not the finalized August 15 validator-list count
- Risk disclosures: <https://docs.raiku.com/legal/disclosures>

### On-chain identifiers and Explorer references

- Sanctum SPL Stake Pool program: `SP12tWFxD9oJsVWNavTTBZvMbA6gkAmxtVgxdqvyvhY`
- Pool state: `ERhozr6u9drmAANXGRNP1oh3quSqPKEwioKH5b8v9Kkt` — <https://explorer.solana.com/address/ERhozr6u9drmAANXGRNP1oh3quSqPKEwioKH5b8v9Kkt>
- rkuSOL mint: `rkubjTrZYioRSeXwDnhwGQzvW3qkcin72JSxUt3WMVp` — <https://explorer.solana.com/address/rkubjTrZYioRSeXwDnhwGQzvW3qkcin72JSxUt3WMVp>
- Validator list: `BtRJM6kHw9hEKZRPtkcNG5F1T5FxZrBwdBzUXzVo8WY2` — <https://explorer.solana.com/address/BtRJM6kHw9hEKZRPtkcNG5F1T5FxZrBwdBzUXzVo8WY2>
- Current vote account: `AVD61fbwxDGuLGCanPWQPxRjdqYk3icssz5u7JH8kbta` — <https://explorer.solana.com/address/AVD61fbwxDGuLGCanPWQPxRjdqYk3icssz5u7JH8kbta>

The finalized pool state encoded a 2.5% epoch/reward fee, 0% SOL and stake deposit fees, and 0.1% fees for both SOL and stake withdrawals. The 0.1% withdrawal fields conflict with Raiku's general no-withdrawal-fee wording. Prefer a dated contract-state reading and fresh transaction preview for rkuSOL-specific costs.

The current one-entry validator list must not be presented as evidence that the historical six-partner pipeline is already live. Pilot access, client installation, a contact inquiry, or a future application also does not guarantee acceptance, rkuSOL allocation, stake amount, duration, AOT/JIT revenue, MEV revenue, APY, or reward pass-through.

## Phase resources and updates

- SFDP analytics: <https://phase.cc/tools/sfdp>
- IPS methodology: <https://phase.cc/delegation/ips>
- SFDP data update: <https://phase.cc/blog/solana-foundation-delegation-program-data>
- Phase validator dashboard: <https://phase.cc/delegation/validators>
- Phase X post: <https://x.com/phase_/status/2067995658779554300> — social/update source only, not primary docs

## Public validator dashboards and tools

- Phase validator dashboard: <https://phase.cc/delegation/validators>
- Edgevana validator list: <https://stake.edgevana.com/validators>
- JPool validators dashboard: <https://app.jpool.one/validators>
- Jito StakeNet Steward: <https://www.jito.network/stakenet/steward/>
- DoubleZero DZDP calculator: <https://doublezero.xyz/dzdp/calculator>
- xSHIN validators page: <https://xshin.fi/#Validators>
- ValidBlocks Stake Pools Heatmap: <https://dashboards.validblocks.com/stakepools-heatmap> — third-party dynamic monitoring dashboard; not official program rules
- ValidBlocks Solana Validators Profitability (SVP): <https://dashboards.validblocks.com/svp> — third-party dynamic monitoring dashboard; per-validator profitability (client, version, commission, Jito/MEV, rewards/costs/profit) with SFDP and vote-lagging filters; replaces the retired `/validators-live` route (checked 2026-07-29)
- ValidBlocks Marinade Select: <https://dashboards.validblocks.com/marinade-select> — third-party dynamic monitoring dashboard; does not imply acceptance, eligibility, or delegation
- ValidBlocks BAM Claims: <https://dashboards.validblocks.com/bam-claims> — third-party dynamic monitoring dashboard; not an official eligibility or delegation guarantee
- Sandwiched.me validators (SFDP filter): <https://sandwiched.me/validators?sort=activeStake_desc&stakeSource=SFDP> — third-party filterable validator directory with client/version, Ghost Score, Slot Time Score, and 30d/60d sandwich percentage; this view filters to SFDP-sourced stake; scores are Sandwiched.me's own methodology, not independently verified

## Vault

- Validator application process: <https://docs.thevault.finance/delegation/validator-application-process>
- Board-gated delegation buckets: <https://docs.thevault.finance/delegation/approved-validators#board-gated-delegation-buckets>

## Marinade / Marinade Select / SAM

- SAM eligibility criteria: <https://docs.marinade.finance/marinade-protocol/protocol-overview/stake-auction-market/eligibility-criteria>
- Marinade Select docs: <https://docs.marinade.finance/marinade-protocol/protocol-overview/marinade-select.md>
- Marinade Select announcement: <https://marinade.finance/blog/marinade-select-unlocking-institutional-staking-on-solana>
- Marinade institutions page: <https://marinade.finance/institutions>
- ValidBlocks Marinade Select dashboard: <https://dashboards.validblocks.com/marinade-select>
- SAM resources: <https://docs.marinade.finance/marinade-protocol/protocol-overview/stake-auction-market/sam-resources.md>
- SAM stake matching: <https://docs.marinade.finance/marinade-protocol/protocol-overview/stake-auction-market/stake-matching.md>
- Validator Bonds agent skills: <https://github.com/marinade-finance/validator-bonds#agent-skills> — official Marinade Validator Bonds repository section for protocol-context agent skills/tooling; tooling/resource reference only and does not imply participation, eligibility, acceptance, delegation, partnership, endorsement, or guaranteed stake

## JPool

- How to join JPool Delegation Program: <https://docs.jpool.one/delegation-strategy/how-to-join-jpool-delegation-program.html>
- Inclusion and removal criteria: <https://docs.jpool.one/delegation-strategy/inclusion-and-removal-criteria.html>
- JPool validators dashboard: <https://app.jpool.one/validators>
- JPool Community Good validator stake application form: <https://docs.google.com/forms/d/e/1FAIpQLSc7GX3g2womS6sGHNZU8cau4K5ZyEmlSZ0ZdrBpKhP86q11tQ/viewform>

## DoubleZero

- DZDP: <https://doublezero.xyz/dzdp>
- DZDP calculator: <https://doublezero.xyz/dzdp/calculator>

## xSHIN / Shinobi

- Strategy: <https://xshin.fi/#Strategy>
- Validators page: <https://xshin.fi/#Validators>

## Jito

- Delegation criteria: <https://www.jito.network/docs/jitosol/jitosol-liquid-staking/stake-pool-operations/delegation-criteria/>
- JIP-28 BAM adoption: <https://forum.jito.network/t/jip-28-accelerate-bam-adoption/904>
- ValidBlocks BAM Claims dashboard: <https://dashboards.validblocks.com/bam-claims>
- StakeNet Steward: <https://www.jito.network/stakenet/steward/>

## Data source note

The research article describes validator counts, approximate stake, and average stake values as based on Validators.app data and rounded for practical comparison. These values should be treated as directional and re-verified before reuse. The rkuSOL monitoring note instead uses the separately dated finalized epoch-1017 pool-state and validator-list snapshot above; it remains outside the 15-program actionable registry.

Programs, dashboards, ranking criteria, application forms, and eligibility requirements can change quickly. Dynamic dashboards should be verified live before reuse. ValidBlocks dashboards are third-party dynamic monitoring sources, not official program rules.

## Disclaimer

These links are provided for research traceability. Listing a source does not imply endorsement, sponsorship, recommendation, official partnership, approval, acceptance, or guaranteed delegation from any pool, program, project, company, or foundation.
