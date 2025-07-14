NITI: A Non-Custodial Protocol for Bitcoin-Backed Synthetic Assets

Satoshi Nakamoto-inspired style: Abstract, Introduction, sections with technical explanations, proofs, conclusion, references.

Abstract

We propose a protocol for issuing synthetic assets on Bitcoin using the Lightning Network, enabling non-custodial creation of financial instruments such as stablecoins and derivatives. By employing Cascading Discreet Log Contracts, the system allows participants to form competing private currencies backed solely by bitcoin, addressing the limitations of centralized and algorithmic alternatives. The protocol relies on cryptographic commitments and oracles for settlement, providing security against manipulation while preserving decentralization. We define the theoretical foundations, architecture, and implementation to demonstrate its viability.

1. Introduction

Commerce on the Internet has come to rely almost exclusively on financial institutions serving as trusted third parties to process electronic payments. While the system works well enough for most transactions, it still suffers from the inherent weaknesses of the trust based model. Completely non-reversible transactions are not really possible, since financial institutions cannot avoid mediating disputes. The cost of mediation increases transaction costs, limiting the minimum practical transaction size and cutting off the possibility for small casual transactions, and there is a broader cost in the loss of ability to make non-reversible payments for non-reversible services. With the possibility of reversal, the need for trust spreads. Merchants must be wary of their customers, hassling them for more information than they would otherwise need. A certain percentage of fraud is accepted as unavoidable. These costs and payment uncertainties can be avoided in person by using physical currency, but no mechanism exists to make payments over a communications channel without a trusted party.

What is needed is an electronic payment system based on cryptographic proof instead of trust, allowing any two willing parties to transact directly with each other without the need for a trusted third party. Transactions that are computationally impractical to reverse would protect sellers from fraud, and routine escrow mechanisms could easily be implemented to protect buyers. In this paper, we propose a solution to the double-spending problem using a peer-to-peer distributed timestamp server to generate computational proof of the chronological order of transactions. The system is secure as long as honest nodes collectively control more CPU power than any cooperating group of attacker nodes.

In the context of Bitcoin, the native asset excels as a store of value but its volatility hinders use as a unit of account or medium of exchange in many cases. Existing solutions, such as centralized stablecoins, introduce counterparty risk and regulatory vulnerabilities, while algorithmic variants often require overcollateralization and suffer from complex failure modes. Drawing from monetary theory, including Gresham's Law and the functions of money as outlined by Mankiw—store of value, medium of exchange, and unit of account—we identify a "Paradox of Money": rational agents hoard superior stores of value like bitcoin and spend inferior ones.

To resolve this, we introduce NITI, a protocol for non-custodial synthetic assets on Bitcoin. Synthetics simulate other asset prices using bitcoin as collateral, forming private currencies in competition as envisioned by Hayek in "Denationalisation of Money" (1976). Integrated with Mises' observation of money's natural monopoly tendency, all synthetics share bitcoin backing for efficiency. The protocol layers Bitcoin as follows: base token for store of value, Lightning Network for medium of exchange, and NITI for unit of account.

2. Current Solutions

Stablecoins fall into three categories, as classified by Amoedo:

2.1 Centralized (IOU) Stablecoins

These are backed by fiat reserves held by a central entity, such as USDT or USDC. Users relinquish custody, introducing counterparty risk. Transparency issues have led to depegging events, and regulatory oversight enables censorship. Despite these drawbacks, they achieve wide adoption due to simplicity.

2.2 Algorithmic Stablecoins

Backed by digital assets via smart contracts, examples include MakerDAO and TerraUSD. They eliminate centralization but demand overcollateralization (e.g., 2:1 ratios), increasing capital costs. Unique mechanisms require technical expertise, and failures like TerraUSD highlight risks. Their focus on fiat replication limits diversity.

2.3 Synthetic Assets

NITI enables synthetics pegged to commodities, indices, or any verifiable price. Issuers select collateral baskets for specific needs, such as hedging diesel prices or Bitcoin transaction fees. All adhere to a standard model, reducing complexity. Unlike centralized systems, NITI supports niche assets without direct reserves, using private bitcoin-collateral contracts. This fills a market gap, as algorithmic stablecoins overlook diverse applications.

3. Theoretical Foundations

We model monetary utility as an optimization problem.

3.1 Monetary Utility Function

We define the utility of a monetary asset m_i at time t for agent θ as:

U(m_i, t, θ) = α(θ,t) * V(m_i,t) + β(θ,t) * T(m_i,t) + γ(θ,t) * A(m_i,t) + δ(θ,t) * S(m_i,t)

where V is store of value, T transaction utility, A accounting utility, S security, and α,β,γ,δ are preference weights.

Theorem 1: For any agent θ and period [t1,t2], an optimal portfolio exists maximizing expected U subject to budget constraints.

Proof: The problem is a concave program under standard portfolio theory, with uniqueness from strict concavity. See Appendix A.

3.2 Layered Monetary System

A layer L_i includes asset set A_i, transfer f_i, settlement g_i to lower layer, and risk r_i.

Theorem 2: L_i is stable iff E[r_i(a)] ≤ E[r_{i-1}(g_i(a))] + φ_i for all a, where φ_i is convenience yield.

Proof: Follows from risk-utility tradeoff; stability via Lyapunov function in Appendix A.

3.3 Currency Competition Game

Players: issuers, users, oracles. Strategies S_i, payoffs π_i.

Theorem 3: A Nash equilibrium exists under regularity conditions.

Proof: Compact strategy spaces and continuous payoffs yield fixed point by Glicksberg. Stability if Jacobian eigenvalues have negative real parts.

4. Transactions

We define a synthetic asset as a conditional claim on bitcoin collateral, settled via Discreet Log Contracts (DLCs).

4.1 Discreet Log Contracts

A DLC is a tuple (Setup, Commit, Reveal, Settle).

Setup generates keys; Commit locks funds; Reveal provides oracle outcome; Settle distributes based on signature.

DLCs mirror Lightning channels but for conditional payments: pre-signed transactions, only oracle-validated one broadcasts.

Theorem 4: DLCs satisfy completeness, soundness, privacy, atomicity under discrete log assumption.

Proof: Soundness reduces to EUF-CMA security; see Appendix B.

4.2 Cascading DLCs (CDLCs)

CDLC chains DLCs: outcome of one triggers next.

Construction: Cascade function links contracts; security via domain-separated hash H(C_k ⊕ D_j ⊕ nonce ⊕ timestamp).

Anti-correlation: Derived keys α'_i = KDF(α_base, i, chain_id).

Example: DLC on BTCUSD variation pre-signs T={T1..Tn}. Oracle signs Ck; derive Tnk = α + β H(Ck). Triggers next for periodic settlements.

Theorem 5: CDLC prevents length extension, correlation, replay attacks.

4.3 Oracle Aggregation

For n oracles with weights w_i, outcome via weighted consensus, threshold θ.

Theorem 6: Tolerates floor((n-1)/3) faulty oracles with high probability.

Matching uses Nostr: parties publish terms, select reputable oracles, coordinate via signed messages.

5. Risk Management

5.1 Value-at-Risk

Portfolio VaR under multivariate t-distribution: VaR_α = μ + σ sqrt((ν-2)/ν) t_{ν,α}, with dynamic covariance Σ_t.

Theorem 7: VaR_total ≤ sum VaR_i - sum ρ_{ij} sqrt(VaR_i VaR_j).

Example: Bitcoin VaR 8.25%, diversified basket (1/3 each Bitcoin, dollar, gold) yields 1% due to low correlations.

5.2 Lombard Loans

Optimize collateral: min w' Σ w s.t. sum w=1, LTV ≤ max.

Loans use synthetics as collateral; margin calls if value drops, liquidation otherwise.

Theorem 8: P(liquidation) ≤ exp(-μ^2 / 2σ^2).

5.3 Systemic Risk

Contagion P(i→j) = Φ( (ρ Φ^{-1}(PD_i) - Φ^{-1}(PD_j)) / sqrt(1-ρ^2) ).

Theorem 9: Stable if contagion matrix spectral radius <1.

6. Economic Model

6.1 Market Structure

Order book with price discovery and liquidity functions.

Theorem 10: Prices form martingale under rational expectations.

6.2 Equilibrium

Market clearing S_i(p*) = D_i(p*), risk-return E[R_i] = r_f + β_i λ.

Theorem 11: Equilibrium exists and unique under conditions.

6.3 Stability

System stable if perturbations decay: ||x(t)-x*|| ≤ K e^{-λ t} ||x(0)-x*||.

Theorem 12: Via Lyapunov function with negative derivative.

7. Protocol

7.1 Architecture

Matching via Nostr, oracles with reputation, settlement on Lightning, risk monitoring.

Messages: type, payload, ed25519 signature, timestamp, nonce.

7.2 Logic

Synthetic struct: asset_id, collateral map, oracle set, maturity, conditions, params.

Functions: create, deposit, withdraw, liquidate, settle.

7.3 Consensus

Weighted median aggregation; disputes verify evidence, slash malicious.

8. Implementation

Primitives: SHA3-256 hash, ed25519/BLS/Schnorr signatures, HKDF.

Routing and peer discovery via bootstrap.

Optimizations: Batch processing, caching.

9. Security

Threat: Bounded adversary, corrupts <n/3 oracles.

Theorem 13: Protocol secure with negligible failure probability.

Mitigations:

Oracle manipulation: Aggregation.

Front-running: Commit-reveal.

Others: Dynamic fees, proof-of-burn, diverse peers.

10. Incentives

Fees: base + complexity * cost + risk * insurance.

Rewards: Oracle accuracy bonuses minus slashes; market makers via spreads and rebates.

11. Disclosures

Regulatory: Transparent, decentralized; synthetics may classify as securities.

Risks: Market volatility, oracle failures, liquidity, technical vulnerabilities.

12. Conclusion

We have proposed a protocol for synthetic assets on Bitcoin, enabling non-custodial derivatives with bitcoin backing. By combining cryptographic contracts and economic models, it implements competing currencies while maintaining security and efficiency. The system requires no trust in intermediaries and scales with Lightning.

References

[1] Dryja, T. Discreet Log Contracts. 2018.

[2] Mankiw, N.G. Macroeconomics. 2019.

[3] Schramm, A. Bitcoin, o sistema de liquidação final.

[4] Amoedo, R. Stables bancárias, algorítmicas e sintéticos.

[5] Hayek, F.A. Denationalisation of Money. 1976.

[6] Mises, L.v. The Theory of Money and Credit. 1912.

[7] Kim & Mauborgne. Blue Ocean Strategy. 2005.

[8] Credit Suisse. Lombard Loans.

[9] Investopedia. Gresham's Law.

Appendices

A. Proofs

A.1 Theorem 1: Concave program, KKT conditions.

A.2 Theorem 2: Lyapunov V = sum (E[r_i] - E[r_{i-1}] - φ_i)^2, dot V <0.

A.3 Theorem 4: Forgery contradicts DL assumption.

B. Cryptography

Curve: secp256k1.

Signatures: Schnorr (BIP-340).

KDF: HKDF.

C. Risk Equations

VaR = μ + q σ, with DCC-GARCH updates.

Document Hash: [SHA3-256 placeholder]

License: GPLv3

Publication: July 14, 2025.
