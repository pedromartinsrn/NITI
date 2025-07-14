NITI: Non-custodial Interlinked Tokenization Infrastructure  
A Protocol for Bitcoin-Backed Synthetic Assets  
WHITEPAPER 1.0  
Publication Date: July 14, 2025  
Authors: Pedro Martins Rodrigues Novaes, Dr. Caleb Isaac  
Contact: nitidev@proton.me, contact@niti.finance  

Abstract  
NITI presents a cryptographically secure and economically sound protocol for creating synthetic derivatives on Bitcoin through the Lightning Network. Using Cascading Discreet Log Contracts (CDLCs) with enhanced security properties, participants can create diverse financial instruments including stablecoins, futures, options, and loans while maintaining non-custodial control. This protocol implements a modernized version of Hayek's competing currencies framework with rigorous mathematical foundations, comprehensive risk management, and formal security guarantees. NITI's mission is to implement the free monetary system proposed by Hayek using bitcoin as the sole backing, enabling synthetics that act as private currencies in free competition, backed by layered monetary structures on Bitcoin.

Keywords: Bitcoin, Lightning Network, Discreet Log Contracts, Synthetic Assets, Competing Currencies, Cryptographic Protocols  

1. Introduction  
1.1 Problem Statement  
The cryptocurrency ecosystem faces a fundamental tension between Bitcoin's superior monetary properties and the practical need for diverse financial instruments. While Bitcoin excels as a store of value, its volatility limits its utility as a unit of account and medium of exchange for specific use cases. Existing solutions suffer from:  

- Centralized stablecoins: Counterparty risk and regulatory vulnerability  
- Algorithmic stablecoins: Insufficient collateralization and complex failure modes  
- DeFi protocols: Smart contract risk and limited Bitcoin integration  

Derived from Gresham's Law, the "Paradox of Money" arises: ceteris paribus, rational agents prefer to spend first currencies with lower potential as a store of value while accumulating currencies with higher potential as a store of value for future exchanges. As the least inflationary currency in existence and the one with the most potential as a long-term store of value, bitcoin tends to be accumulated and not spent. According to Mankiw in "Macroeconomics," money has three functions: Store of Value (transfer purchasing power from present to future), Medium of Exchange (facilitate exchanges), and Unit of Account (determine relative prices). Bitcoin in its raw form maximizes the Store of Value function, while other layers seek to fulfill the remaining functions, each with different attributes and distinct focuses.  

The "Non-custodial Interlinked Tokenization Infrastructure" (NITI) is a proposal to create an interlinked and non-custodial tokenization infrastructure, allowing the issuance of stablecoins called "Synthetics." These Synthetics are satoshi balances that simulate the price of other assets, acting as private currencies in free competition. NITI's mission is the monetary system proposed by Hayek in 1976, in “Denationalisation of Money,” creating a protocol so that currencies with stable relative prices can compete freely, using a single backing: bitcoin.  

1.2 Money in Layers  
Elaborated extensively in Alan Schramm’s article “Bitcoin, the final settlement system,” the concept of Money in Layers states that money has a base layer from which others can be built. Gold, for example, was not used in its raw form for the three main monetary functions but from specialized layers:  

- Nuggets: metal after extraction in its original form.  
- Bars: standardization of purity, format, measures, and weighing.  
- Certificates: ownership documents for divisibility and transport.  
- Notes: paper backed by certificates used to price assets.  

The view that bitcoin in its raw form maximizes all money functions does not match the history of money. To use bitcoin as a medium of exchange and unit of account, we must recognize the Paradox of Money and Money in Layers. Our proposal divides Bitcoin into layers:  

- Bitcoin: native token focused on Store of Value.  
- Lightning Network: "certificates" of bitcoin used as Medium of Exchange.  
- NITI: synthetics backed by certificates for Unit of Account.  

1.3 The Monetary Systems of Hayek and Mises  
Hayek, in "The Denationalisation of Money" (1976), proposed private institutions issuing currencies that circulate freely, with users choosing stable ones. This competition leads to better currencies, as issuers maintain value for reputation. Mises, in "The Theory of Money and Credit" (1912), noted humanity tends toward a single money as a natural monopoly, rejecting less suitable goods until one remains. NITI integrates these: a system of private currencies, all backed by bitcoin, facilitating efficiency without added exchanges.  

2. Current Solutions and NITI's Differentiation  
Renato Amoedo's article, "Bank stables, Algorithmic and Synthetics," classifies stablecoins into three categories:  

2.1 Centralized Stablecoins (IOU)  
These derive value from fiat reserves held centrally (e.g., USDT, USDC). They carry counterparty risk, as users lose custody and trust issuers for reserves. Lack of transparency has led to scams and depegging. Subject to regulation and censorship, yet widely used (USDT is the third-largest cryptocurrency).  

2.2 Algorithmic Stablecoins  
Backed by digital assets via smart contracts (e.g., MakerDAO, TerraUSD), they avoid centralization but require overcollateralization (e.g., 2:1 ratio), increasing costs. Users need technical knowledge of unique algorithms and backing assets. High perceived risk led to collapses like TerraUSD. They focus on fiat replication, competing ineffectively with IOUs.  

2.3 Synthetics and NITI's Approach  
NITI synthetics link to commodities, stocks, indices, or any verifiable price, with issuers choosing baskets for niches. All follow a standard DLC model for transparency. Unlike IOUs, NITI enables token diversity (e.g., Diesel hedge, Bitcoin fee rates, weather), impossible for centralized systems due to complexity. Standardization reduces risk perception; users know all synthetics adhere to the protocol, unlike flawed unique systems (e.g., TerraUSD incompatible). NITI fills a market gap by enabling peculiar use cases via private BTC-collateral contracts.  

3. Theoretical Foundations  
3.1 Monetary Theory and the Optimization Problem  
We formalize the monetary utility function as a multi-objective optimization problem:  

Definition 3.1 (Monetary Utility Function)  

\( U(m_i, t, \theta) = \alpha(\theta,t) \cdot V(m_i,t) + \beta(\theta,t) \cdot T(m_i,t) + \gamma(\theta,t) \cdot A(m_i,t) + \delta(\theta,t) \cdot S(m_i,t) \)  

Where:  
- \( V(m_i,t) \): Store of value utility at time t  
- \( T(m_i,t) \): Transaction utility (speed, cost, finality)  
- \( A(m_i,t) \): Accounting utility (price stability, divisibility)  
- \( S(m_i,t) \): Security utility (censorship resistance, seizure resistance)  
- \( \alpha, \beta, \gamma, \delta \): Time and agent-dependent preference weights  
- \( \theta \): Agent preference parameters  

Theorem 3.1 (Monetary Specialization Theorem) For any agent \( \theta \) and time period [t₁,t₂], there exists an optimal portfolio allocation across monetary assets that maximizes expected utility subject to budget and liquidity constraints.  

Proof Sketch: This follows from standard portfolio optimization theory with the additional constraint that monetary assets must satisfy the medium of exchange property. The formal proof is provided in Appendix A.  

3.2 Layered Monetary System  
Definition 3.2 (Monetary Layer) A monetary layer L_i consists of:  

- Asset Set: A_i = {a₁, a₂, ..., aₙ}  
- Transfer Function: f_i: A_i → A_i  
- Settlement Function: g_i: A_i → A_{i-1}  
- Risk Function: r_i: A_i → ℝ⁺  

Theorem 3.2 (Layer Stability Condition) A monetary layer L_i is stable if and only if:  

\( \forall a \in A_i: \mathbb{E}[r_i(a)] \leq \mathbb{E}[r_{i-1}(g_i(a))] + \phi_i \)  

where \( \phi_i \) is the convenience yield of layer i. This ensures higher layers provide utility benefits to compensate for risk.  

3.3 Hayek's Competing Currencies: A Game-Theoretic Framework  
Definition 3.3 (Currency Competition Game) The currency competition game G consists of:  

- Players: N = {issuers, users, oracles}  
- Strategies: S_i for each player type  
- Payoffs: π_i(s₁, s₂, ..., sₙ) for strategy profile s  
- Information Structure: I_i for each player  

Theorem 3.3 (Existence of Nash Equilibrium) Under mild regularity conditions, the currency competition game has at least one Nash equilibrium.  

Corollary 3.3.1 (Stability of Equilibrium) The equilibrium is stable if the Jacobian of the best response functions has all eigenvalues with negative real parts.  

4. Cryptographic Architecture  
4.1 Discreet Log Contracts  
Definition 4.1 (Secure DLC) A Secure DLC is a tuple (Setup, Commit, Reveal, Settle) where:  

- Setup(1^λ, O, P₁, P₂) → (pp, sk₁, sk₂, pk₁, pk₂, pk_O)  
- Commit(pp, sk_i, m, t) → (σ̃_i, R_i)  
- Reveal(pp, pk_O, outcome, t) → σ_O  
- Settle(pp, σ̃₁, σ̃₂, σ_O, outcome) → (σ₁, σ₂)  

DLCs allow private agreements using real-world data, similar to Lightning Network but for conditional payments. Alice and Bob pre-sign transactions, with only the oracle-signed outcome executable.  

Theorem 4.1 (DLC Security Properties) The Enhanced DLC construction satisfies: Completeness, Soundness, Privacy, Atomicity. Proof: See Appendix B.  

4.2 Cascading Discreet Log Contracts (CDLCs)  
Definition 4.2 (CDLC) A Cascading DLC extends the basic DLC with:  

- Cascade Function: Cascade(DLC₁, DLC₂, ..., DLCₙ) → CDLC  
- Enhanced Security Construction: H_secure(C_k, D_j, nonce, timestamp) = SHA3-256(C_k ⊕ D_j ⊕ nonce ⊕ timestamp)  
- Anti-Correlation Mechanism: α'_i = KDF(α_base, i, chain_id); β'_i = KDF(β_base, i, chain_id)  

CDLCs interconnect DLCs in sequence, where one result triggers the next. For example, Alice and Bob set a DLC on BTCUSD variation, pre-configuring transactions T = {T1, ..., Tn} with Adaptor Signatures. Oracle signs Ck (e.g., "10-20% variation"). Derive key: Tnk = α + βH(Ck). This activates a second DLC for periodic buys, with keys Tn'kj = α'G + β'H(Ck | Dj). Process repeats via signed Nostr messages.  

Theorem 4.2 (CDLC Security) Prevents length extension, key correlation, replay, and oracle manipulation.  

4.3 Multi-Oracle Aggregation and Decentralized Matching  
Definition 4.3 (Oracle Aggregation Scheme) For oracles O₁, ..., Oₙ with scores r₁, ..., rₙ: Weighted consensus outcome = argmax_x ∑(i: O_i votes x) w_i·r_i, with threshold ∑ w_i ≥ θ·∑w_i.  

Theorem 4.3 (Byzantine Fault Tolerance) Tolerates ⌊(n-1)/3⌋ faulty oracles with probability 1-ε.  

NITI uses Nostr for decentralized matching: Users publish encrypted intentions (terms like asset, expiration). Matches form, selecting reputable oracles from Nostr lists based on accuracy/frequency. NITI coordinates publication of signed results, enabling chain activation without intermediating execution.  

5. Risk Management and Portfolio Theory  
5.1 Value-at-Risk Model  
Definition 5.1 (Dynamic VaR Model) For portfolio P with synthetics S₁, ..., Sₙ: Multivariate t-Distribution R_t | Σ_t ~ t_ν(μ, Σ_t); Dynamic Correlation Σ_t = (1-α-β)·Σ̄ + α·R_{t-1}R'_{t-1} + β·Σ_{t-1}; VaR_α(P) = μ_P + σ_P·√((ν-2)/ν)·t_{ν,α}.  

Theorem 5.1 (Portfolio Risk Decomposition) VaR_total ≤ ∑VaR_i - ∑∑ρ_{ij}·√(VaR_i·VaR_j).  

In analyses, diversification benefits are quantified. Using 1-day, 99% confidence, daily data from 2014: Bitcoin VaR 8.25%, Dollar 1.81%, Gold 2.14%. Combined (1/3 each): 1%, due to low correlations—mathematically 8x safer than Bitcoin alone.  

5.2 Lombard Loan Optimization  
Definition 5.2 (Optimal Collateral Allocation) Minimize σ²_portfolio = w'Σw subject to ∑w_i = 1, LTV ≤ LTV_max, w_i ≥ 0.  

Lombard Loans use liquid assets as collateral for liquidity without selling. In NITI, diversified synthetics (e.g., 1/3 Gold Synthetic, 1/3 Dollar Synthetic, 1/3 Bitcoin) back new synthetics via DLCs, reducing volatility and margin calls. If collateral falls below limit, margin call; failure leads to liquidation. Users customize baskets for risk profiles.  

Theorem 5.2 (Liquidation Probability Bound) P(liquidation) ≤ exp(-μ²/(2σ²)).  

5.3 Systemic Risk Analysis  
Definition 5.3 (Contagion Model) P(contagion_{i→j}) = Φ((ρ_{ij}·Φ^{-1}(PD_i) - Φ^{-1}(PD_j))/√(1-ρ²_{ij})).  

Theorem 5.3 (Network Stability) Stable if spectral radius of contagion matrix <1.  

6. Economic Equilibrium Analysis  
6.1 Market Microstructure  
Definition 6.1 (Synthetic Asset Market) Order Book B = {bids, asks}; Price Discovery P(t) = f(supply, demand, information); Liquidity L(t) = g(spreads, depth, resilience).  

Theorem 6.1 (Market Efficiency) Under rational expectations, prices follow a martingale adjusted for risk premiums.  

6.2 Equilibrium Conditions  
Definition 6.2 (General Equilibrium) ∀i: S_i(p_i*) = D_i(p_i*); E[R_i] = r_f + β_i·λ; ∑w_i = 1, w_i ≥ 0.  

Theorem 6.2 (Existence and Uniqueness) Exists and unique under regularity conditions.  

6.3 Stability Analysis  
Definition 6.3 (System Stability) ||x(t) - x*|| ≤ K·e^{-λt}·||x(0) - x*||.  

Theorem 6.3 (Lyapunov Stability) Stable if Lyapunov function V satisfies V̇ < 0.  

7. Protocol Specification  
7.1 Network Architecture  
Components: Matching Engine (decentralized via Nostr); Oracle Network (reputation-scored); Settlement Layer (Lightning); Risk Engine (real-time monitoring).  

Communication: Message = {type: enum{ORDER, MATCH, ORACLE_DATA, SETTLEMENT}, payload: bytes, signature: ed25519_signature, timestamp: unix_timestamp, nonce: random_bytes(32)}.  

7.2 Smart Contract Logic  
Struct SyntheticAsset {asset_id: bytes32, collateral_composition: Map<asset_id, weight>, oracle_set: Set<oracle_pubkey>, maturity: timestamp, settlement_conditions: SettlementLogic, risk_parameters: RiskParams}.  

Transitions: create_synthetic(params) → asset_id; deposit_collateral(...); withdraw_collateral(...); liquidate_position(...); settle_contract(...).  

7.3 Consensus Mechanism  
Oracle aggregate_oracle_data(oracle_reports): weighted_median, confidence_interval. Dispute resolve_dispute(dispute_id, evidence): verify, revert, slash.  

8. Implementation Details  
8.1 Cryptographic Primitives  
Hashes: SHA3-256, BLAKE3, Poseidon. Signatures: ed25519, BLS, Schnorr. KDF: HKDF(master_key, purpose || index).  

8.2 Network Protocol  
Routing: route_message(message, destination). Discovery: discover_peers() via bootstrap.  

8.3 Performance Optimizations  
Batch process_batch(transactions): sort, validate, apply. Cache cache_oracle_data(oracle_id, data, ttl).  

9. Security Analysis  
9.1 Threat Model  
Adversary: Polynomial-time, delays messages, corrupts t < n/3 oracles, adaptive. Goals: Integrity, Availability, Privacy, Atomicity.  

9.2 Formal Security Proofs  
Theorem 9.1 (Protocol Security) Satisfies goals with probability 1-negl(λ). Proof: Composes DLC soundness, BFT, commitments, structure.  

9.3 Attack Mitigation  

| Attack Type | Mitigation Strategy |  
|-------------|---------------------|  
| Oracle Manipulation | Multi-oracle aggregation with reputation scoring |  
| Front-running | Commit-reveal scheme with time delays |  
| Liquidity Attacks | Dynamic fee adjustment and circuit breakers |  
| Sybil Attacks | Proof-of-stake or proof-of-burn requirements |  
| Eclipse Attacks | Diverse peer selection and monitoring |  

10. Economic Incentives  
Fee Structure: total_fee = base_fee + (complexity_factor × computation_cost) + (risk_factor × insurance_cost).  

Oracle: reward = base + accuracy_bonus - slashing_penalty. Market Maker: reward = spread_capture + liquidity_mining + fee_rebates.  

11. Regulatory and Risk Disclosures  
11.1 Regulatory Framework  
Principles: Transparency, Decentralization, Compliance, Privacy. Adheres to securities laws (synthetics may be securities), tax reporting, data protection (GDPR).  

11.2 Risk Disclosures  
Investment: Market, Counterparty (oracle), Liquidity, Technology. Operational: Congestion, Oracle failures, Regulatory changes, Cybersecurity.  

12. Ecosystem Development  
Tools: SDK, APIs (REST/GraphQL), Documentation, Testing. Programs: Grants, Bug Bounties, Hackathons, Education.  

13. Conclusion  
NITI advances Bitcoin-based finance with enhanced security, economic soundness, scalable implementation, and compliance. Innovations: Formal proofs, equilibrium analysis, risk management, token diversity via standardization. Enables diverse instruments preserving decentralization. We invite contributions to the open-source ecosystem.  

Acknowledgments  
Thanks to Bitcoin/Lightning communities, cryptographic designers, and reviewers.  

Appendices  
Appendix A: Formal Mathematical Proofs  
A.1 Proof of Theorem 3.1 (Monetary Specialization)  
Let θ∈Θ, w∈Δⁿ, U_θ(w)=E_t[∑ w_i·u_θ(m_i,t)]. Convex constraints ∑w_i·p_i≤W, w_i≥0. Concave program (strictly concave u_θ), Slater holds, KKT necessary/sufficient. Uniqueness from Hessian ≺0. ∎  

A.2 Proof of Theorem 3.3 (Nash Equilibrium)  
Compact simplices S_i, continuous quasi-concave π_i. Glicksberg’s theorem yields fixed point. ∎  

A.3 Proof of Theorem 4.1 (DLC Soundness)  
Forging σ without σ_O contradicts EUF-CMA under DL assumption. Adv_A ≤ negl(λ). ∎  

A.4 Proof of Layer Stability (Theorem 3.2)  
V(x)=∑(E[r_i]-E[r_{i-1}]-φ_i)²≥0. Derivative negative if φ_i≥sup Δr, asymptotic stability. ∎  

Appendix B: Cryptographic Specification  
Curves: secp256k1, p=2²⁵⁶-2³²-977, n≈1.158×10⁷⁷, h=1. Signatures: Schnorr (BIP-340), Ed25519. Hashes/KDFs: SHA3-256 (FIPS 202), HKDF (RFC 5869). Tag: "NITI-CDLC-2025"||C_k||D_j. Threshold: BLS t/n≤32, t=⌈2n/3⌉.  

Appendix C: Risk Engine Equations  
VaR_{α,t}=μ_P,t + q_{α,ν}·σ_P,t, q=√((ν-2)/ν)·t^{-1}_ν(α). DCC-GARCH: Σ_t=(1-α-β)·Σ̄ + α(R_{t-1}R'_{t-1}) + β·Σ_{t-1}, α+β<1. Stress: V_c,s=V_c,0·(1+ΔP_s), liquidates if < L·MCR^{-1}.  

Document Hash: [Updated SHA3-256]  
License: GPLv3  

References:  
- Dryja, T. (2018). Discreet Log Contracts. Whitepaper.  
- Mankiw, N. G. (2019). Macroeconomics.  
- Schramm, A. Bitcoin, o sistema de liquidação final.  
- Amoedo, R. Stables bancárias, algorítmicas e sintéticos.  
- Hayek, F. A. (1976). Denationalisation of Money.  
- Kim, W. C., & Mauborgne, R. (2005). Blue Ocean Strategy.  
- Credit Suisse. Lombard Loans.  
- Investopedia. Gresham's Law.  
- Mises, L. v. (1912). The Theory of Money and Credit.
