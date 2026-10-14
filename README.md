<!-- solve-problem:1eb738e2-1c68-4174-a88a-ec2c25ca0d8a -->
# Difficulty-upgrade incentive conflicts

A [Tangle Solve problem](https://solve.tangle.tools/problems/1eb738e2-1c68-4174-a88a-ec2c25ca0d8a).

## What is the problem?

In Proof-of-Work blockchains, the difficulty adjustment algorithm (DAA) — e.g., Bitcoin's 2016-block retarget — sets the mining hardness target as a function of recent block timestamps. Existing DAAs can be manipulated: miners can strategically distort timestamps (timestamp attacks) or strategically enter/exit (difficulty swings from hash-rate volatility), and the resulting volatility in block times is not just a technical nuisance but a *distributional* one: some miners profit from it (e.g., late-night/low-difficulty mining, "cheat mining" as studied by Ilie et al.; large miners who benefit from oscillations; renters of hash power who time entry to under-adjusted difficulty).

The problem: **design (and analyze adoption of) a more stable DAA when the parties who must adopt it — miners, via consensus-rule changes (soft/hard forks) or hash-power voting — include agents who are net beneficiaries of current volatility.** Formally: model miners as strategic players with private hash power and private valuations over DAAs; the protocol upgrade is a collective-choice/bargaining problem with veto players (sufficient hash power or stake can block a fork). The task is to (a) characterize the set of stable DAAs (robust to timestamp manipulation and participation shocks — see Ilie et al.'s game-theoretic DAA analysis), and (b) determine whether an incentive-compatible adoption path exists from a legacy volatile DAA to a stable one, accounting for strategic blocking, and design it if so.

Ambiguity note: the census record is a one-line future-work item; the precise model (who votes, what threshold, what utility function over volatility) is not fixed and must be formalized by the solver.

## Why does it matter?

Every PoW chain inherits DAA pathologies: timestamp manipulation, difficulty oscillations from coin-hopping/rental hash, degraded fee markets and confirmation-time predictability. A stability-plus-adoption theory would tell developers whether better DAAs (like Ilie et al.'s game-theoretically robust alternatives) are *deployable* or forever blocked by incumbent miners — the political-economy question underlying every protocol upgrade. Downstream: safer hard-fork planning, better designs for new chains, and a bridge between mechanism design and consensus-layer engineering.

## What's already known?

- Ilie, Sholander and Sandmann (2021, arXiv:2006.03044) analyze Bitcoin's DAA game-theoretically, show timestamp manipulation and "cheat mining" are profitable under the legacy rule, and propose DAAs robust to these attacks (using moving averages / median timestamps). This addresses *technical* stability, not *adoption* incentives.
- Noda, Okumura and Hashimoto (2026) (verify — journal may not be accessible) reportedly provide an economic analysis of DAAs quantifying miner payoffs under volatility and list this adoption/adversary problem as explicit future work.
- Classic context: Carlsten et al. (2016) on incentive instability as block rewards decline; Kiayias et al. and Leshno–Strack on blockchain forks as coordination/committee formation; the bargaining-with-veto literature (e.g., Barberá–Jackson, Binmore–Rubinstein) for the blocking analysis.
- Gap: no work models DAA *upgrades* as a bargaining problem among profit-from-volatility miners. This is the open territory.

## What would count as solving it?

1. **Model + impossibility or possibility result.** A formal game where a legacy DAA prevails and a stable DAA is on the table; prove either (a) no incentive-compatible adoption mechanism exists when a coalition with hash share > threshold profits from volatility, or (b) construct a mechanism (fork design, side-chain bridge, reward-side transfer to compensate losers) implementing the upgrade in equilibrium.
2. **Characterization:** identify conditions on miner valuation dispersion / hash concentration under which stable DAAs are adoptable (e.g., a threshold on the volatility-rent share of total revenue).
3. **Applied validation:** simulation or empirical calibration (historical difficulty/rental-hash data) showing the mechanism's blocking conditions hold or fail on real chains.

## How to start

1. Read Ilie et al. (2021) §on cheat mining and their proposed robust DAA — this gives the utility-from-volatility primitive you need.
2. Try to obtain Noda–Okumura–Hashimoto (DOI 10.1111/iere.70028) (verify) for their formal model and the exact future-work statement.
3. Build the minimal model: two DAAs (legacy, stable), n miners with hash shares αᵢ, utilities uᵢ(DAA); upgrade requires hash majority q. First question: when is the stable DAA a core outcome / when does a blocking coalition form?
4. Main obstacle: endogenous volatility payoffs — a miner's gain from volatility depends on others' participation, coupling the DAA choice to a participation game (cf. Carlsten et al.). Solve the two-miner case first.

## Key references

- Ilie, A., Sholander, S., Sandmann, J. (2021). *Bitcoin's Difficulty Adjustment Algorithm: A Game-Theoretic Analysis*. arXiv:2006.03044. https://arxiv.org/abs/2006.03044 — Shows timestamp manipulation and cheat mining are profitable under Bitcoin's DAA and proposes game-robust alternatives.
- Noda, S., Okumura, T., Hashimoto, T. (2026). *An Economic Analysis of Difficulty Adjustment Algorithms in Proof-of-Work Blockchain Systems*. DOI:10.1111/iere.70028 (verify; accessibility uncertain) — Economic analysis of DAA-induced miner payoffs; source of the open problem statement.
- Carlsten, M., Wust, A., Campbell, A., van Engelshoven, S. (2016). *On the Instability of Bitcoin Without the Block Reward*. CCS '16 — Foundational model of miner participation/fee incentives relevant to volatility payoffs. (verify exact author list)
- Leshno, C., Strack, P. (2020). *Bitcoin: An Impossibility Theorem for PoW* — Fork-choice and miner-coordination modeling methodology. (verify)

## Warnings

- The 2026 citation is forward-dated from the census source; treat its content as unverified until you read it — do not assume its model.
- The problem statement is genuinely underspecified: no voting rule, utility model, or threat point is fixed. Choosing a defensible formalization is part of the contribution; state it explicitly.
- Common dead end: analyzing DAA stability in isolation (already done by Ilie et al.) without the adoption/bargaining layer — that's the known part, not the open part.
- Don't conflate "miners prefer high difficulty volatility" with "miners prefer any volatility"; specify the payoff channel (entry timing, timestamp manipulation, rental hash) precisely or results won't generalize.

---
*`BCGT-000247` · unverified*

## Acceptance guidance

1. **Model + impossibility or possibility result.** A formal game where a legacy DAA prevails and a stable DAA is on the table; prove either (a) no incentive-compatible adoption mechanism exists when a coalition with hash share > threshold profits from volatility, or (b) construct a mechanism (fork design, side-chain bridge, reward-side transfer to compensate losers) implementing the upgrade in equilibrium.
2. **Characterization:** identify conditions on miner valuation dispersion / hash concentration under which stable DAAs are adoptable (e.g., a threshold on the volatility-rent share of total revenue).
3. **Applied validation:** simulation or empirical calibration (historical difficulty/rental-hash data) showing the mechanism's blocking conditions hold or fail on real chains.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/1eb738e2-1c68-4174-a88a-ec2c25ca0d8a?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: BCGT-000247.

- [Public source catalog](https://drewstone.github.io/problems/#/p/BCGT-000247)
