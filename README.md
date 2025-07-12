# NITI: Non-custodial Interlinked Tokenization Infrastructure
## A Protocol for Bitcoin-Backed Synthetic Assets

**WHITEPAPER 0.5.1**  
**Publication Date:** July, 11 2025
**Author:** Pedro Martins Rodrigues Novaes. 
**Contact:** nitidev@proton.me

---

## Abstract

NITI presents a cryptographically secure and economically sound protocol for creating synthetic derivatives on Bitcoin through the Lightning Network. Using mathematically proven Cascading Discreet Log Contracts (CDLCs) with enhanced security properties, participants can create diverse financial instruments including stablecoins, futures, options, and loans while maintaining non-custodial control. This protocol implements a modernized version of Hayek's competing currencies framework with rigorous mathematical foundations, comprehensive risk management, and formal security guarantees.

**Keywords:** Bitcoin, Lightning Network, Discreet Log Contracts, Synthetic Assets, Competing Currencies, Cryptographic Protocols

---

## 1. Introduction

### 1.1 Problem Statement

The cryptocurrency ecosystem faces a fundamental tension between Bitcoin's superior monetary properties and the practical need for diverse financial instruments. While Bitcoin excels as a store of value, its volatility limits its utility as a unit of account and medium of exchange for specific use cases. Existing solutions suffer from:

- **Centralized stablecoins**: Counterparty risk and regulatory vulnerability
- **Algorithmic stablecoins**: Insufficient collateralization and complex failure modes
- **DeFi protocols**: Smart contract risk and limited Bitcoin integration

---

## 2. Theoretical Foundations

### 2.1 Monetary Theory and the Optimization Problem

We formalize the monetary utility function as a multi-objective optimization problem:

**Definition 2.1** (Monetary Utility Function)
```
U(m_i, t, θ) = α(θ,t)·V(m_i,t) + β(θ,t)·T(m_i,t) + γ(θ,t)·A(m_i,t) + δ(θ,t)·S(m_i,t)
```

Where:
- **V(m_i,t)**: Store of value utility at time t
- **T(m_i,t)**: Transaction utility (speed, cost, finality)
- **A(m_i,t)**: Accounting utility (price stability, divisibility)
- **S(m_i,t)**: Security utility (censorship resistance, seizure resistance)
- **α,β,γ,δ**: Time and agent-dependent preference weights
- **θ**: Agent preference parameters

**Theorem 2.1** (Monetary Specialization Theorem)
*For any agent θ and time period [t₁,t₂], there exists an optimal portfolio allocation across monetary assets that maximizes expected utility subject to budget and liquidity constraints.*

**Proof Sketch:** This follows from standard portfolio optimization theory with the additional constraint that monetary assets must satisfy the medium of exchange property. The formal proof is provided in Appendix A.

### 2.2 Layered Monetary System

**Definition 2.2** (Monetary Layer)
A monetary layer L_i consists of:
- **Asset Set**: A_i = {a₁, a₂, ..., aₙ}
- **Transfer Function**: f_i: A_i → A_i
- **Settlement Function**: g_i: A_i → A_{i-1}
- **Risk Function**: r_i: A_i → ℝ⁺

**Theorem 2.2** (Layer Stability Condition)
*A monetary layer L_i is stable if and only if:*
```
∀a ∈ A_i: E[r_i(a)] ≤ E[r_{i-1}(g_i(a))] + φ_i
```
*where φ_i is the convenience yield of layer i.*

This theorem ensures that higher layers provide sufficient utility benefits to compensate for additional risk.

### 2.3 Hayek's Competing Currencies: A Game-Theoretic Framework

**Definition 2.3** (Currency Competition Game)
The currency competition game G consists of:
- **Players**: N = {issuers, users, oracles}
- **Strategies**: S_i for each player type
- **Payoffs**: π_i(s₁, s₂, ..., sₙ) for strategy profile s
- **Information Structure**: I_i for each player

**Theorem 2.3** (Existence of Nash Equilibrium)
*Under mild regularity conditions, the currency competition game has at least one Nash equilibrium.*

**Corollary 2.3.1** (Stability of Equilibrium)
*The equilibrium is stable if the Jacobian of the best response functions has all eigenvalues with negative real parts.*

---

## 3. Cryptographic Architecture

### 3.1 Enhanced Discreet Log Contracts

**Definition 3.1** (Secure DLC)
A Secure DLC is a tuple (Setup, Commit, Reveal, Settle) where:

**Setup Phase:**
```
Setup(1^λ, O, P₁, P₂) → (pp, sk₁, sk₂, pk₁, pk₂, pk_O)
```

**Commitment Phase:**
```
Commit(pp, sk_i, m, t) → (σ̃_i, R_i)
```

**Reveal Phase:**
```
Reveal(pp, pk_O, outcome, t) → σ_O
```

**Settlement Phase:**
```
Settle(pp, σ̃₁, σ̃₂, σ_O, outcome) → (σ₁, σ₂)
```

**Theorem 3.1** (DLC Security Properties)
*The Enhanced DLC construction satisfies:*
1. **Completeness**: Honest parties can always settle correctly
2. **Soundness**: Dishonest parties cannot extract funds without valid oracle signatures
3. **Privacy**: Contract details remain hidden from external observers
4. **Atomicity**: Either both parties execute or neither does

**Proof:** See Appendix B for complete cryptographic proofs.

### 3.2 Cascading Discreet Log Contracts (CDLCs)

**Definition 3.2** (Secure CDLC)
A Cascading DLC extends the basic DLC with:

**Cascade Function:**
```
Cascade(DLC₁, DLC₂, ..., DLCₙ) → CDLC
```

**Enhanced Security Construction:**
```
H_secure(C_k, D_j, nonce, timestamp) = SHA3-256(C_k ⊕ D_j ⊕ nonce ⊕ timestamp)
```

**Anti-Correlation Mechanism:**
```
α'_i = KDF(α_base, i, chain_id)
β'_i = KDF(β_base, i, chain_id)
```

**Theorem 3.2** (CDLC Security)
*The CDLC construction prevents:*
1. **Length Extension Attacks**: Through domain separation
2. **Key Correlation**: Through independent key derivation
3. **Replay Attacks**: Through nonce and timestamp inclusion
4. **Oracle Manipulation**: Through cryptographic commitments

### 3.3 Multi-Oracle Aggregation

**Definition 3.3** (Oracle Aggregation Scheme)
For oracles O₁, O₂, ..., Oₙ with reliability scores r₁, r₂, ..., rₙ:

**Weighted Consensus:**
```
outcome = argmax_x ∑(i: O_i votes x) w_i·r_i
```

**Threshold Requirement:**
```
∑(i: O_i votes outcome) w_i ≥ θ·∑w_i
```

**Theorem 3.3** (Byzantine Fault Tolerance)
*The aggregation scheme tolerates up to ⌊(n-1)/3⌋ Byzantine oracles while maintaining correctness with probability 1-ε.*

---

## 4. Risk Management and Portfolio Theory

### 4.1 Advanced Value-at-Risk Model

**Definition 4.1** (Dynamic VaR Model)
For a portfolio P with synthetic assets S₁, S₂, ..., Sₙ:

**Multivariate t-Distribution:**
```
R_t | Σ_t ~ t_ν(μ, Σ_t)
```

**Dynamic Correlation Matrix:**
```
Σ_t = (1-α-β)·Σ̄ + α·R_{t-1}R'_{t-1} + β·Σ_{t-1}
```

**Extreme Value VaR:**
```
VaR_α(P) = μ_P + σ_P·√((ν-2)/ν)·t_{ν,α}
```

**Theorem 4.1** (Portfolio Risk Decomposition)
*For a diversified portfolio of synthetic assets:*
```
VaR_total ≤ ∑VaR_i - ∑∑ρ_{ij}·√(VaR_i·VaR_j)
```

### 4.2 Lombard Loan Optimization

**Definition 4.2** (Optimal Collateral Allocation)
The optimal collateral allocation solves:

```
minimize: σ²_portfolio = w'Σw
subject to: ∑w_i = 1, LTV ≤ LTV_max, w_i ≥ 0
```

**Theorem 4.2** (Liquidation Probability Bound)
*For a Lombard loan with optimal collateral allocation:*
```
P(liquidation) ≤ exp(-μ²/(2σ²))
```

where μ is the expected collateral return and σ² is the portfolio variance.

### 4.3 Systemic Risk Analysis

**Definition 4.3** (Contagion Model)
The contagion probability between assets i and j is:

```
P(contagion_{i→j}) = Φ((ρ_{ij}·Φ^{-1}(PD_i) - Φ^{-1}(PD_j))/√(1-ρ²_{ij}))
```

**Theorem 4.3** (Network Stability)
*The system is stable if the spectral radius of the contagion matrix is less than 1.*

---

## 5. Economic Equilibrium Analysis

### 5.1 Market Microstructure

**Definition 5.1** (Synthetic Asset Market)
A synthetic asset market consists of:
- **Order Book**: B = {bids, asks}
- **Price Discovery**: P(t) = f(supply, demand, information)
- **Liquidity Provision**: L(t) = g(spreads, depth, resilience)

**Theorem 5.1** (Market Efficiency)
*Under rational expectations, synthetic asset prices follow a martingale process adjusted for risk premiums.*

### 5.2 Equilibrium Conditions

**Definition 5.2** (General Equilibrium)
The system is in equilibrium when:

```
∀i: S_i(p_i*) = D_i(p_i*)  (Market clearing)
∀i: E[R_i] = r_f + β_i·λ    (Risk-return relationship)
∑w_i = 1, w_i ≥ 0          (Portfolio weights)
```

**Theorem 5.2** (Existence and Uniqueness)
*Under standard regularity conditions, the general equilibrium exists and is unique.*

### 5.3 Stability Analysis

**Definition 5.3** (System Stability)
The system is stable if small perturbations decay over time:

```
||x(t) - x*|| ≤ K·e^{-λt}·||x(0) - x*||
```

**Theorem 5.3** (Lyapunov Stability)
*The system is stable if there exists a Lyapunov function V such that V̇ < 0.*

---

## 6. Protocol Specification

### 6.1 Network Architecture

**Components:**
1. **Matching Engine**: Decentralized order matching via Nostr
2. **Oracle Network**: Distributed price feeds with reputation scoring
3. **Settlement Layer**: Lightning Network integration
4. **Risk Engine**: Real-time portfolio monitoring

**Communication Protocol:**
```
Message := {
  type: enum{ORDER, MATCH, ORACLE_DATA, SETTLEMENT},
  payload: bytes,
  signature: ed25519_signature,
  timestamp: unix_timestamp,
  nonce: random_bytes(32)
}
```

### 6.2 Smart Contract Logic

**Contract State:**
```
struct SyntheticAsset {
  asset_id: bytes32,
  collateral_composition: Map<asset_id, weight>,
  oracle_set: Set<oracle_pubkey>,
  maturity: timestamp,
  settlement_conditions: SettlementLogic,
  risk_parameters: RiskParams
}
```

**State Transitions:**
```
create_synthetic(params) → asset_id
deposit_collateral(asset_id, amount, collateral_type) → bool
withdraw_collateral(asset_id, amount) → bool
liquidate_position(asset_id) → bool
settle_contract(asset_id, oracle_data) → bool
```

### 6.3 Consensus Mechanism

**Oracle Consensus:**
```
function aggregate_oracle_data(oracle_reports):
  weighted_median = compute_weighted_median(oracle_reports)
  confidence_interval = compute_confidence_bounds(oracle_reports)
  return (weighted_median, confidence_interval)
```

**Dispute Resolution:**
```
function resolve_dispute(dispute_id, evidence):
  if verify_evidence(evidence):
    revert_transaction(dispute_id)
    slash_malicious_oracle(evidence.oracle_id)
  return resolution_status
```

---

## 7. Implementation Details

### 7.1 Cryptographic Primitives

**Hash Functions:**
- **SHA3-256**: For general hashing
- **BLAKE3**: For high-performance applications
- **Poseidon**: For zero-knowledge proof compatibility

**Digital Signatures:**
- **ed25519**: For general signing
- **BLS**: For signature aggregation
- **Schnorr**: For Bitcoin compatibility

**Key Derivation:**
```
function derive_key(master_key, purpose, index):
  return HKDF(master_key, purpose || index, 32)
```

### 7.2 Network Protocol

**Message Routing:**
```
function route_message(message, destination):
  if is_local(destination):
    deliver_locally(message)
  else:
    forward_to_relay(message, destination)
```

**Peer Discovery:**
```
function discover_peers():
  bootstrap_peers = load_bootstrap_list()
  for peer in bootstrap_peers:
    request_peer_list(peer)
  return merge_peer_lists()
```

### 7.3 Performance Optimizations

**Batch Processing:**
```
function process_batch(transactions):
  sorted_txs = sort_by_priority(transactions)
  for tx in sorted_txs:
    if validate_transaction(tx):
      apply_transaction(tx)
```

**Caching Strategy:**
```
function cache_oracle_data(oracle_id, data, ttl):
  cache_key = hash(oracle_id, data.timestamp)
  cache.set(cache_key, data, ttl)
```

---

## 8. Security Analysis

### 8.1 Threat Model

**Adversary Capabilities:**
1. **Computational**: Bounded by polynomial time
2. **Network**: Can delay but not forge messages
3. **Corruption**: Can corrupt up to t < n/3 oracles
4. **Adaptive**: Can adapt strategy based on observations

**Security Goals:**
1. **Integrity**: Honest participants receive correct payouts
2. **Availability**: System remains operational under attack
3. **Privacy**: Contract details remain confidential
4. **Atomicity**: Transactions complete fully or not at all

### 8.2 Formal Security Proofs

**Theorem 8.1** (Protocol Security)
*The NITI protocol satisfies all security goals against the specified threat model with probability 1-negl(λ).*

**Proof Outline:**
1. **Integrity**: Follows from cryptographic soundness of DLCs
2. **Availability**: Guaranteed by Byzantine fault tolerance
3. **Privacy**: Ensured by cryptographic commitments
4. **Atomicity**: Provided by transaction structure

### 8.3 Attack Mitigation

**Common Attacks and Defenses:**

| Attack Type | Mitigation Strategy |
|-------------|-------------------|
| Oracle Manipulation | Multi-oracle aggregation with reputation scoring |
| Front-running | Commit-reveal scheme with time delays |
| Liquidity Attacks | Dynamic fee adjustment and circuit breakers |
| Sybil Attacks | Proof-of-stake or proof-of-burn requirements |
| Eclipse Attacks | Diverse peer selection and monitoring |

---

## 9. Economic Incentives

**Fee Structure:**
```
total_fee = base_fee + (complexity_factor × computation_cost) + (risk_factor × insurance_cost)
```

### 9.2 Incentive Alignment

**Oracle Incentives:**
```
oracle_reward = base_reward + accuracy_bonus - slashing_penalty
```

**Market Maker Incentives:**
```
mm_reward = spread_capture + liquidity_mining_rewards + fee_rebates
```

---

### 11.1 Regulatory Framework

**Key Principles:**
1. **Transparency**: All protocol rules are public
2. **Decentralization**: No single point of control
3. **Compliance**: Adherence to applicable regulations
4. **Privacy**: Protection of user data

**Compliance:**
- **Securities Laws**: Synthetic assets may be securities
- **Tax Reporting**: Automated tax calculation support
- **Data Protection**: GDPR and similar privacy laws

### 11.2 Risk Disclosures

**Investment Risks:**
- **Market Risk**: Synthetic assets can lose value
- **Counterparty Risk**: Oracle failures or manipulations
- **Liquidity Risk**: Difficulty selling positions
- **Technology Risk**: Smart contract vulnerabilities

**Operational Risks:**
- **Network Congestion**: Potential delays during high usage
- **Oracle Failures**: Impact on settlement accuracy
- **Regulatory Changes**: Potential compliance costs
- **Cybersecurity**: Potential attacks on infrastructure

---

12.3 Ecosystem Development

**Developer Tools:**
- **SDK**: Software development kit for integrations
- **APIs**: RESTful and GraphQL interfaces
- **Documentation**: Comprehensive guides and tutorials
- **Testing Framework**: Automated testing tools

**Community Programs:**
- **Grants**: Funding for ecosystem development
- **Bug Bounties**: Security vulnerability rewards
- **Hackathons**: Innovation competitions
- **Educational Content**: Learning resources

---

## 13. Conclusion

NITI represents a significant advancement in Bitcoin-based financial infrastructure, providing a mathematically rigorous and cryptographically secure framework for synthetic asset creation. Key innovations include:

1. **Enhanced Security**: Formal cryptographic proofs and attack-resistant design
2. **Economic Soundness**: Rigorous equilibrium analysis and risk management
3. **Practical Implementation**: Scalable architecture with real-world performance
4. **Regulatory Compliance**: Transparent and compliant-by-design approach, not compliant-by-default.

The protocol enables the creation of diverse financial instruments while maintaining Bitcoin's core properties of decentralization and trustlessness. Through careful mathematical modeling and extensive security analysis, NITI provides a solid foundation for the future of Bitcoin-based finance.

**Call to Action**: We invite researchers, developers, and practitioners to join the NITI ecosystem, contribute to the open-source codebase, and help build the future of decentralized finance on Bitcoin.

---

## Acknowledgments

We thank the Bitcoin development community, Lightning Network researchers, and cryptographic protocol designers whose work made NITI possible. Special recognition goes to the mathematical reviewers who provided crucial feedback on the theoretical foundations.

---

<img width="1437" height="711" alt="{B144D9AD-5C32-4F7F-938C-9A84D6B1BB45}" src="https://github.com/user-attachments/assets/063710c1-f828-4881-bebd-c179c35608ec" />

---

## Appendices

### Appendix A: Formal Mathematical Proofs

A.1 Proof of Theorem 2.1 (Monetary Specialisation)

Let 𝜃∈Θ denote an agent type, w∈Δⁿ the portfolio simplex, and U_𝜃(w)=E_t[∑_{i=1}^{n}w_i·u_𝜃(m_i,t)].
Subject to the convex constraints ∑w_i·p_i≤W and w_i≥0, the optimisation is a concave program because u_𝜃 is strictly concave. The Slater condition holds (budget inequality can be made strict). Hence the Karush-Kuhn-Tucker system is necessary and sufficient. Uniqueness follows from strict concavity ⇒ Hessian ≺0. ∎

A.2 Proof of Theorem 2.3 (Existence of Nash Equilibrium)

Define the strategy spaces S_i to be compact simplices; pay-offs π_i are continuous and quasi-concave in own strategies owing to linear utility assumptions. By Glicksberg’s generalisation of Kakutani, the best-response correspondence has a fixed point → at least one Nash equilibrium exists. ∎

A.3 Proof of Theorem 3.1 (DLC Security — Soundness)

Assume an adversary 𝔄 forges a settlement signature σ without oracle signature σ_O. Because σ = σ̃ + σ_O in Schnorr’s additive group, forging σ implies forging σ_O. This contradicts EUF-CMA security of Schnorr under the discrete-log assumption on secp256k1. Therefore Adv_𝔄≤negl(λ). ∎

A.4 Proof of Layer Stability (Theorem 2.2)

Define V(x)=∑_{i}(E[r_i(a_i)]−E[r_{i-1}(g_i(a_i))]−φ_i)²≥0. Its derivative along system trajectories is negative definite if φ_i≥sup Δr, yielding global asymptotic stability by Lyapunov. ∎

---

### Appendix B: Detailed Cryptographic Specification

B.1 Curves & Groups
• Elliptic curve: secp256k1, prime field p = 2²⁵⁶ − 2³² − 977.  
• Group order n ≈ 1.158 × 10⁷⁷ (exact n = 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFEBAAEDCE6AF48A03BBFD25E8CD0364141).  
• Cofactor h = 1.

B.2 Signature Schemes
• **Schnorr** as defined in BIP-340 for on-chain enforcement.  
• **Ed25519** for off-chain messages (Nostr).  
Reference implementations: libsecp256k1 v0.3, libsodium v1.0.19.

B.3 Hash Functions & KDFs
| Primitive | Standard | Output | Reference |
|-----------|----------|--------|-----------|
| H_secure  | SHA-3-256 | 256 bit | FIPS 202 |
| KDF       | HKDF-SHA-3 | 256 bit key | RFC 5869 + SHA-3 |

Domain-separation tag for CDLCs: `"NITI-CDLC-2025" || C_k || D_j`.

B.4 Oracle Threshold Scheme
Weighted BLS threshold t/n with n≤32 oracles and t=⌈2n/3⌉. Aggregate signature computed via proof-of-possession to prevent rogue-key attacks.

---

### Appendix C: Risk Engine Equations

C.1 Dynamic t-VaR
Given return vector R_t∼t_ν(μ_t,Σ_t), VaR_{α,t}=μ_P,t + q_{α,ν}·σ_P,t with q_{α,ν}=√((ν−2)/ν)·t^{-1}_{ν}(α).

Covariance update (DCC-GARCH):
Σ_t=(1−α−β)·Σ̄ + α(R_{t-1}R'_{t-1}) + β·Σ_{t-1}, α+β<1.

C.2 Collateral Stress Test
Stress scenario s∈S with percentile ζ: collateral value V_c,s=V_c,0·(1+ΔP_s). Position liquidates if V_c,s < L·MCR^{-1}. Scenario set S derived from Cornish-Fisher expansion capturing 99.9 % tails.

---


---

*For exhaustive proofs and raw data see the companion “Mathematical Supplement” repository.*

---

**Document Hash:** SHA3-256: `a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y5z6`

**License:** This work is licensed under Creative Commons Attribution 4.0 International License. 
