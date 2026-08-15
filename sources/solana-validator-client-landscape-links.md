# Source Links — Solana Validator Client Landscape

Status checked: 2026-07-29

Quantumglow sources checked: 2026-08-05

FireBAM and Raiku sources checked: 2026-08-15

Editorially updated: 2026-08-15

Companion source list for:

- `articles/solana-validator-client-landscape.md`
- Website article: https://solanaqubits.com/research/solana-validator-client-landscape

This source index follows the website article’s evidence hierarchy. Official repositories and documentation are primary classification sources. Dashboards, methodology pages, visualizations, and secondary profiles provide context but require careful interpretation of labels, filters, identity methods, and denominators. The 2026-08-05 Quantumglow check and 2026-08-15 FireBAM/Raiku check are scoped updates; they do not re-date the overall client and dashboard snapshot from 2026-07-29.

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
  Primary source for the full Firedancer versus Frankendancer distinction. Its README retains older wording that full Firedancer is not ready for test or production use and has no full release; this conflicts with the newer official release artifacts below.

- Firedancer releases
  https://github.com/firedancer-io/firedancer/releases
  Official release artifacts. The release feed lists full Firedancer Mainnet v1.1.4 as mainnet ready, updated 2026-08-10, and Frankendancer v0.1105.40200 updated 2026-08-11. Preserve this artifact-specific conflict with the README, and do not infer network-wide adoption from a tagged release.

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

### Alpenglow and post-quantum protocol research

- Anza — Quantumglow: will Solana's performance survive quantum computing?
  https://www.anza.xyz/blog/quantumglow-will-solana%E2%80%99s-performance-survive-quantum-computing
  Official Anza research overview for Quantumglow's proposed post-quantum adaptation of Alpenglow, Ax signatures, local certificate events, block commitments, and the stated performance evidence.

- Alpenglow whitepaper v1.2
  https://drive.google.com/file/d/1RPJ9OyohFMuFfLmTB5ydPYlrKTIlUxq9/view
  Primary protocol-design source for Alpenglow and the Quantumglow construction. It is research documentation, not a validator-client release or activation decision.

- Distributed Quorum Signatures preprint
  https://arxiv.org/abs/2607.17700
  Primary formal-analysis source for the distributed-quorum-signature construction and supporting evidence. Formal analysis, simulations, and microbenchmarks are not mainnet or production measurements.

- Anza — Securing Solana against a powerful quantum adversary
  https://www.anza.xyz/blog/securing-solana-against-a-powerful-quantum-adversary
  Official scope source explaining that post-quantum migration reaches beyond consensus into accounts, transaction authorization, validator identities, networking, and programs.

### Schedulers, block-building, and orderflow systems

- BAM overview
  https://bam.dev/docs/bam/bam-overview/
  Official Blockspace Assembly Marketplace architecture source. BAM is block assembly and scheduler infrastructure, not a consensus client or validator client.

- BAM for validators
  https://bam.dev/validators/
  Current validator-facing source for permissionless access, leader-schedule requirements, and the two documented paths: Jito-Solana and FireBAM for Firedancer/Frankendancer-derived operation. It also documents the startup requirement for the bundle and BAM tiles and the external scheduler/TEE boundary. Generic audit language on this page is not a substitute for a linked FireBAM-specific final report.

- FireBAM announcement
  https://bam.dev/blog/introducing-firebam-bam-expands-to-firedancer/
  Official 2026-05-13 announcement describing FireBAM as a Frankendancer-compatible BAM client, testnet/mainnet availability, early third-party onboarding, the vendor-stated incentive extension, and an Asymmetric Research audit then in progress. Announcement claims and planned follow-up are point-in-time, not guarantees.

- FireBAM repository
  https://github.com/jito-foundation/firebam
  Primary source describing FireBAM as a fork of Firedancer that adds BAM validator support. This supports a Firedancer/Frankendancer-derived fork/distribution classification, not a new independent implementation.

- FireBAM releases
  https://github.com/jito-foundation/firebam/releases
  Official FireBAM artifacts. The feed lists Firedancer Mainnet 1.1.4 on 2026-08-11 and Frankendancer Mainnet v0.1105.40200 on 2026-08-14, both labeled mainnet ready. They correspond to upstream release lines and add the BAM distribution path; release metadata is not network-wide adoption evidence.

- FireBAM setup guide
  https://jito-foundation.gitbook.io/mev/jito-solana/firebam-setup-guide
  Official setup source for the FireBAM path. It is operational documentation, not evidence of completed deployment, incentive eligibility, revenue, or stake.

### Raiku

- Raiku website
  https://raiku.com/
  First-party product overview for Raiku's AOT compute reservations and JIT MEV bundle processing. Product and performance descriptions remain vendor-stated.

- Raiku validators page
  https://raiku.com/validators
  First-party operator page describing potential validator economics and advertising participation. Its documented public form was unavailable when checked, so the page is not evidence of a working intake, acceptance, client access, deployment, revenue, coverage, or adoption.

- Raiku documentation
  https://docs.raiku.com/
  Official documentation entry point for the client, Engine, validator integration, staking product, and roadmap.

- Raiku validator quickstart
  https://docs.raiku.com/validator-quickstart
  Primary architecture and access-status source. It says `raiku-agave` is built on `jito-agave`, can coexist with Jito Classic, is not compatible with Jito BAM, is available to pilot partners, and is intended to be open-sourced after the pilot.

- Raiku features
  https://docs.raiku.com/features
  First-party description of the external Engine, AOT/JIT marketplaces, bundle routing, configurable Raiku commission, and onchain Merkle-root-based tip distribution.

- Raiku configuration
  https://docs.raiku.com/configuration
  Primary source for Jito flag inheritance, external Engine configuration, validator-identity Engine-auth signing, independent Raiku versus Jito commission settings, no-Raiku-bundle behavior when the Engine URL is omitted, and BAM incompatibility. Operational endpoints and key material should not be copied into general research.

- Raiku SDK endpoints
  https://docs.raiku.com/sdk
  First-party endpoint table using `engine.mainnet.raiku.sh`, which conflicts with the quickstart's `engine.mainnet.raiku.ssh` example. Confirm the endpoint directly before production use.

- Raiku troubleshooting
  https://docs.raiku.com/troubleshooting
  First-party fallback and monitoring source. Stub mode preserves ordinary Agave-based validation when the Engine connection is unavailable, but Raiku bundles and associated rewards stop.

- Raiku milestones and roadmap
  https://docs.raiku.com/milestones-and-roadmap
  First-party roadmap that still describes a 2026 mainnet launch as a future stage. This conflicts with the later vendor launch post and should remain visible rather than being silently reconciled.

- Raiku engineering update — Part II
  https://raiku.com/blog/the-engineering-contract-part-ii-how-the-rewrite-works
  Vendor post dated 2026-08-10 saying the client is live on Solana mainnet, Raiku's validator is active, and integrations are rolling out across named operators. It also limits coverage to slots whose assigned leader runs Raiku. This review does not independently verify every named operator deployment.

- Raiku audit reports
  https://docs.raiku.com/audit-reports
  First-party page claiming OtterSec audits of the onchain program and Raiku Agave client and embedding two reports. Audits are point-in-time reviews, not guarantees of safety, availability, or correct deployment.

- Raiku Agave repository URL referenced by the quickstart
  https://github.com/raiku-protocol/raiku-agave
  Returned 404 in an unauthenticated public check on 2026-08-15. Do not infer whether it is private, moved, or removed; record the access conflict alongside the pilot/open-source wording and mainnet claim.

- Raiku validator application instructions
  https://docs.raiku.com/apply-1
  Official page linking to the public validator form. Keep it as a dated application record rather than a working intake claim.

- Raiku validator form
  https://forms.raiku.com/earn_with_raiku
  Returned HTTP 404 when checked on 2026-08-15. Do not present it as an open public application route.

- Raiku contact
  https://raiku.com/contact-us
  Working first-party general contact. Treat it only as an inquiry channel, not an application, admission route, review SLA, deployment confirmation, or rkuSOL allocation promise.

- Raiku Discord
  https://discord.com/invite/raikucom
  Community channel linked from Raiku's official site. It can be used to ask about current pilot access but is not evidence of application or acceptance.

- rkuSOL documentation
  https://docs.raiku.com/staking/rkusol
  First-party description of the Raiku-branded LST built on Sanctum stake-pool infrastructure, validator allocation, auto-compounding, and fee statements. Sanctum provides the LST and stake-pool infrastructure; Raiku says it takes no fee from either staking rewards or Raiku fees attributable to rkuSOL stake and that Sanctum charges 2.5% on staking rewards. These terms are vendor-stated and dynamic, not a promised APY or proof of validator-client adoption.

- Raiku staking FAQ
  https://docs.raiku.com/staking/staking-faqs
  First-party descriptions of staking, MEV, and AOT/JIT reward sources, validator commissions, and product fees. Re-check current terms before reuse; no yield or revenue is guaranteed.

- Raiku staking app
  https://stake.raiku.com/
  Current product entry point for rkuSOL/native-stake context. It is not a validator-operator acceptance path or evidence of delegation to a specific validator.

- Rakurai validator page
  https://rakurai.io/validators
  First-party validator page used for product and onboarding context. Product and economic statements should remain attributed to Rakurai.

- Rakurai documentation
  https://docs.rakurai.io/docs/services/rakurai_jito_private/readme
  First-party source for Rakurai-Solana architecture and incentive descriptions.

- Rakurai validator repository
  https://github.com/rakurai-io/rakurai-validator
  Primary source for Rakurai’s validator fork lineage and repository context.

- Rakurai transaction inclusion guide
  https://docs.rakurai.io/docs/services/rakurai_jito_private/rakurai_docs/transaction_inclusion/transaction_inclusion
  First-party guide for searchers, block engines, and partners describing bundle support across multiple block engines, the virtual priority boost mechanism, and post-pack confirmations. Vendor-stated mechanism description, not independently verified adoption.

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

- Sandwiched.me client distribution
  https://sandwiched.me/clients
  Per-client stake share, validator counts, top validator, and version fragmentation, checked with a stated 704-validator/428.4M SOL denominator. Its Weighted Ghost Score and sandwich-rate labels are Sandwiched.me's own methodology, not independently verified.

### Secondary historical context

- Paladin on Solana Compass
  https://solanacompass.com/projects/paladin
  Secondary project profile sourced from The Grid. It is not first-party evidence of current status, endorsement, or adoption.

## Use notes

- Keep Quantumglow outside validator-client classification and adoption rows. It is post-quantum protocol research, not a fork, executable client release, deployed upgrade, or evidence that the full Solana stack is currently quantum-resistant.
- Keep Jito-Solana classified as a fork/distribution and BAM classified as adjacent infrastructure.
- Keep BAM beside its compatible Jito-Solana and FireBAM paths while making clear that BAM is not a consensus client.
- Classify FireBAM as a Firedancer/Frankendancer-derived BAM fork/distribution. Its tags correspond to upstream release lines; do not portray them as substitutes for upstream releases or infer network-wide adoption from either repository's artifacts.
- Preserve the official Firedancer artifact conflict: the README retains older not-ready/no-full-release wording, while the official release feed lists full Firedancer Mainnet v1.1.4 as mainnet ready. Do not collapse those into a single undated readiness claim.
- Treat Firedancer Reports labels as dashboard-labeled rather than independently confirmed full Firedancer production adoption.
- Keep Raiku distinct from Rakurai. Classify Raiku as a `jito-agave`-derived distribution plus an external AOT/JIT marketplace and Engine, not as an independent consensus implementation.
- Preserve Raiku's source conflicts: the vendor's 2026-08-10 mainnet/rollout statement, the pilot/future language in current docs, and the 404 public repository and application-form checks. Contact and Discord are inquiry-only; do not infer permissionless source availability, acceptance, deployment, rkuSOL allocation, or broad adoption.
- Keep Raiku's explicit incompatibility with Jito BAM visible. Treat AOT/JIT, operator, coverage, integration, commission, and performance statements as vendor-stated unless independently supported.
- Treat rkuSOL as a separate Raiku-branded LST relationship on Sanctum stake-pool infrastructure, with smart-contract, liquidity, allocation, fee, and integration risks; it is not proof of validator-client adoption or guaranteed yield.
- Treat FireBAM and Raiku audit references as point-in-time review evidence, not safety, deployment, performance, or economic guarantees.
- Do not combine instance telemetry, filtered samples, pool heatmaps, behavior indexes, and network graphs into a single adoption percentage.
- Re-check dynamic dashboards and project documentation before external reuse.
- Listing a repository, page, dashboard, or form does not imply endorsement, partnership, official approval, eligibility, acceptance, stake, delegation, APY, earnings, or guaranteed outcomes.
