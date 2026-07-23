# Source Links — Solana Validator Client Landscape

Status checked: 2026-07-22

Editorially updated: 2026-07-23

Companion source list for:

- `articles/solana-validator-client-landscape.md`
- Website article: https://solanaqubits.com/research/solana-validator-client-landscape

This source index follows the website article’s evidence hierarchy. Official repositories and documentation are primary classification sources. Dashboards, methodology pages, visualizations, and secondary profiles provide context but require careful interpretation of labels, filters, identity methods, and denominators.

## Primary repositories and official documentation

### Core validator clients and implementation lineages

- Agave repository
  https://github.com/anza-xyz/agave
  Active Anza-maintained Solana validator client repository used for production-baseline, lineage, release, language, and license context.

- Archived Solana Labs repository
  https://github.com/solana-labs/solana
  Historical validator repository used for archived lineage context, not as the current production branch.

- Jito-Solana repository
  https://github.com/jito-foundation/jito-solana
  Primary source for Jito-Solana as a Solana validator fork/distribution with MEV-oriented integration, not a from-scratch consensus implementation.

- Firedancer repository
  https://github.com/firedancer-io/firedancer
  Primary source for the full Firedancer versus Frankendancer distinction and readiness wording. The repository says full Firedancer is not ready for test or production use and has no full release.

- Firedancer documentation
  https://docs.firedancer.io/
  Official Firedancer documentation entry point.

- Jump Crypto — Firedancer
  https://jumpcrypto.com/build/firedancer
  Official Jump Crypto project page describing Firedancer and linking the Firedancer ecosystem resources.

- Sig repository
  https://github.com/Syndica/sig
  Primary repository for Syndica’s independent Zig Solana validator implementation effort.

- TinyDancer repository
  https://github.com/tinydancer-io/tinydancer
  Primary repository for the TinyDancer light client; it is not a validator block-production client.

### Schedulers, block-building, and orderflow systems

- BAM overview
  https://bam.dev/docs/bam/bam-overview/
  Official Blockspace Assembly Marketplace architecture source. BAM is block assembly and scheduler infrastructure, not a consensus client or validator client.

- BAM for validators
  https://bam.dev/validators/
  Official validator-facing configuration page with documented mainnet/testnet URLs and integration notes.

- Rakurai validator page
  https://rakurai.io/validators
  First-party validator page used for product and onboarding context. Product and economic statements should remain attributed to Rakurai.

- Rakurai documentation
  https://docs.rakurai.io/docs/services/rakurai_jito_private/readme
  First-party source for Rakurai-Solana architecture and incentive descriptions.

- Rakurai validator repository
  https://github.com/rakurai-io/rakurai-validator
  Primary source for Rakurai’s validator fork lineage and repository context.

- Harmonic documentation
  https://docs.harmonic.gg/
  Official entry point for Harmonic’s block-building architecture.

- Harmonic validator page
  https://harmonic.gg/validators
  First-party description of Harmonic validator integrations, Salsa, and Samba.

- Harmonic application form
  https://form.typeform.com/to/UlJMfbPH
  Application/onboarding path only. The form is not evidence of acceptance, stake, delegation, revenue, or other outcomes.

- Harmonic Salsa repository
  https://github.com/harmonic/salsa
  Primary repository for Harmonic’s Agave-derived validator fork.

- Harmonic Samba repository
  https://github.com/harmonic/samba
  Primary repository for Harmonic’s Firedancer/Frankendancer-derived validator fork.

- Flowra documentation
  https://flowra.gitbook.io/flowra
  First-party Open Orderflow Auction documentation used for architecture and roadmap context. Roadmap language is not independent confirmation of launch or adoption.

- Paladin repository
  https://github.com/paladin-bladesmith/paladin-solana
  Primary repository for Paladin’s Jito-derived validator fork and historical context.

### Official adjacent infrastructure documentation

- Solana stake-weighted QoS guide
  https://solana.com/developers/guides/advanced/stake-weighted-qos
  Official Solana guide for SWQoS, classified as network/QoS infrastructure rather than a validator client.

## Dashboard, methodology, and secondary context

### Validator-client labels and telemetry

- Firedancer Reports
  https://reports.firedancer.io/
  Dashboard with filtered validator labels. Treat entries as dashboard-labeled, not independently confirmed as full Firedancer production adoption.

- Firedancer GUI
  https://gui.firedancer.io/
  Validator-instance telemetry. Instance-specific stake is not network-wide client adoption.

- Blockworks validator clients dashboard
  https://blockworks.com/analytics/solana/solana-supply-staking-and-validators/solana-validator-clients
  Secondary client-label context; do not infer independent implementations or network-wide truth without disclosed methodology.

- Blockworks validator clients dashboard v2
  https://blockworks.com/analytics/solana/solana-supply-staking-and-validators/solana-validator-clients-2
  Secondary dashboard used for labels that include hybrid or deprecated categories.

### Block-building methodology and network visualization

- IBRL methodology
  https://ibrl.wtf/methodology
  Methodology for block-building behavior and execution-quality scoring, not validator-client market share.

- IBRL API documentation
  https://ibrl.wtf/api-docs/
  Public API documentation for observable block and validator behavior endpoints.

- Encapsulate Solana mainnet graph
  https://graph.solana.mainnet.encapsulate.xyz/
  Exploratory network visualization. Do not publish exact adoption figures from it without visible methodology and denominator details.

### Stake-pool movement and decentralisation methodology

- ValidBlocks stake-pool heatmap
  https://dashboards.validblocks.com/stakepools-heatmap
  Pool-specific stake movement context, not validator-client adoption.

- ValidBlocks Firedancer pool heatmap
  https://dashboards.validblocks.com/stakepools-heatmap?pool=FIREDANCER
  Firedancer pool-specific heatmap; it is not evidence of full Firedancer client adoption.

- GD Index validator page
  https://gdindex.app/validator
  Geographic decentralisation index for validator location and network context, not client-implementation share.

- GD Index repository
  https://github.com/esterhuizen/sgdi
  Open-source repository and methodology context for GD Index.

### Secondary historical context

- Paladin on Solana Compass
  https://solanacompass.com/projects/paladin
  Secondary project profile sourced from The Grid. It is not first-party evidence of current status, endorsement, or adoption.

## Use notes

- Keep Jito-Solana classified as a fork/distribution and BAM classified as adjacent infrastructure.
- Keep BAM beside Jito-Solana in summaries because BAM integrates with the Jito validator stack, while making clear that BAM is not a consensus client.
- Give the official Firedancer repository readiness statement priority over ambiguous dashboard labels.
- Treat Firedancer Reports labels as dashboard-labeled rather than independently confirmed full Firedancer production adoption.
- Do not combine instance telemetry, filtered samples, pool heatmaps, behavior indexes, and network graphs into a single adoption percentage.
- Re-check dynamic dashboards and project documentation before external reuse.
- Listing a repository, page, dashboard, or form does not imply endorsement, partnership, official approval, eligibility, acceptance, stake, delegation, APY, earnings, or guaranteed outcomes.
