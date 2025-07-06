# Scholarly Impact Network (SIN) - Smart Contract

## Overview

The Scholarly Impact Network (SIN) is a comprehensive blockchain-based platform designed to revolutionize academic publishing and research reputation management. Built on the Stacks blockchain using Clarity smart contracts, SIN provides a decentralized, transparent, and verifiable system for tracking scholarly publications, managing citation networks, and calculating research impact metrics.

## Core Features

### Academic Publication Registry
- **Immutable Publication Storage**: Register scholarly works with comprehensive metadata including title, abstract, discipline, and DOI
- **Author Attribution**: Permanent record of lead authors and co-authors
- **Institutional Verification**: Optional verification system for publication authenticity
- **Timestamp Tracking**: Blockchain-based publication timestamps for priority claims

### Citation Network Management
- **Transparent Citation Tracking**: Establish verifiable citation relationships between publications
- **Contextual Annotations**: Add detailed context and commentary to citations
- **Impact Weighting**: Assign impact weights (1-10) to citations based on relevance and quality
- **Citation Type Classification**: Categorize citations by type (supportive, critical, methodological, etc.)

### Research Impact Analytics
- **Citation Metrics**: Track incoming citations, citation scores, and impact factors
- **H-Index Calculation**: Automated calculation of researcher h-index approximations
- **Discipline-Specific Analytics**: Field-specific impact tracking and comparative metrics
- **Reputation Scoring**: Dynamic reputation system based on citation analytics and verification

### Token-Based Reward System
- **Citation Rewards**: Authors earn tokens when their work is cited
- **Impact-Based Rewards**: Higher impact citations generate more tokens
- **Institutional Bonuses**: Verified publications receive additional reputation bonuses
- **Claimable Rewards**: Researchers can claim accumulated reward tokens

## Architecture

### Data Structures

#### Publications
```clarity
{
  title: (string-ascii 256),
  lead-author: principal,
  publication-timestamp: uint,
  academic-discipline: (string-ascii 64),
  research-abstract: (string-utf8 1024),
  institutional-verification: bool,
  doi-identifier: (optional (string-ascii 128))
}
```

#### Citation Network
```clarity
{
  citation-timestamp: uint,
  contextual-annotation: (optional (string-utf8 256)),
  impact-weight: uint,
  citation-type: (string-ascii 32)
}
```

#### Researcher Profiles
```clarity
{
  total-publications: uint,
  total-citations-received: uint,
  reputation-score: uint,
  verified-publications: uint,
  primary-research-field: (optional (string-ascii 64))
}
```

## Getting Started

### Prerequisites
- Stacks wallet (Hiro Wallet, Xverse, etc.)
- STX tokens for transaction fees
- Basic understanding of blockchain transactions

### Contract Deployment
1. Deploy the contract to the Stacks blockchain
2. The deployer becomes the contract administrator
3. Set up institutional verification authorities as needed

### Basic Usage

#### 1. Submit a Publication
```clarity
(submit-scholarly-publication
  "paper-2024-001"  ;; unique paper ID
  "Revolutionary Blockchain Applications in Academic Publishing"  ;; title
  "Computer Science"  ;; discipline
  "This paper explores the potential of blockchain technology..."  ;; abstract
  (some "10.1000/example.doi"))  ;; optional DOI
```

#### 2. Establish Citation Links
```clarity
(establish-citation-link
  "paper-2024-002"  ;; citing paper
  "paper-2024-001"  ;; referenced paper
  (some "This foundational work demonstrates...")  ;; annotation
  u8  ;; impact weight (1-10)
  "supportive")  ;; citation type
```

#### 3. Verify Publications (Institutional Authority Required)
```clarity
(verify-publication-authenticity "paper-2024-001")
```

#### 4. Claim Reward Tokens
```clarity
(claim-research-rewards)
```

## Query Functions

### Publication Information
- `get-publication-details`: Retrieve complete publication metadata
- `get-publication-metrics`: Get citation counts and impact metrics
- `analyze-citation-network`: Comprehensive citation analysis

### Researcher Analytics
- `get-researcher-profile`: View complete researcher profile
- `calculate-h-index`: Get researcher's h-index approximation
- `calculate-impact-score`: Calculate comprehensive impact score
- `get-reward-balance`: Check available reward tokens

### Network Analysis
- `get-citation-details`: Examine specific citation relationships
- `get-discipline-analytics`: Field-specific statistics and metrics

## Security Features

### Validation Framework
- **Input Validation**: Comprehensive validation of all user inputs
- **Format Verification**: Ensures proper formatting of paper IDs, titles, and abstracts
- **Principal Validation**: Prevents zero-address and invalid principal usage

### Access Control
- **Author Authorization**: Only paper authors can establish citations from their work
- **Administrative Functions**: Critical functions restricted to contract administrator
- **Institutional Verification**: Separate authority system for publication verification

### Anti-Abuse Measures
- **Self-Citation Prevention**: Authors cannot cite their own work
- **Duplicate Prevention**: Prevents duplicate publications and citations
- **Impact Weight Limits**: Citation impact weights constrained to reasonable ranges (1-10)

## Institutional Verification

### Setup Process
1. Administrator authorizes institutional addresses
2. Institutions receive verification privileges
3. Institutions can verify publication authenticity
4. Verified publications receive reputation bonuses

### Benefits
- **Enhanced Credibility**: Institutional verification adds credibility to publications
- **Reputation Bonuses**: Verified publications increase author reputation scores
- **Trust Network**: Builds a web of institutional trust in the academic network

## Economics

### Token Distribution
- **Citation Rewards**: 1-10 tokens per citation (based on impact weight)
- **Verification Bonuses**: 50 tokens for institutional verification
- **Base Reputation**: 100 reputation points for new researchers

### Incentive Alignment
- **Quality Over Quantity**: Higher impact citations provide more rewards
- **Institutional Participation**: Bonuses for verified publications encourage institutional adoption
- **Long-term Value**: Reputation scores accumulate over time, rewarding sustained contributions

## Administrative Functions

### Contract Administration
- `authorize-verification-institution`: Grant verification privileges
- `revoke-verification-authority`: Remove verification privileges
- System configuration and parameter management

### Governance
- Centralized administration for initial deployment
- Potential for future decentralized governance implementation
- Transparent parameter management

## Use Cases

### Academic Researchers
- **Publication Management**: Maintain immutable record of scholarly work
- **Citation Tracking**: Monitor how work is being cited and used
- **Reputation Building**: Build verifiable academic reputation
- **Reward Earning**: Earn tokens for impactful research

### Institutions
- **Publication Verification**: Verify authenticity of affiliated publications
- **Researcher Assessment**: Evaluate researchers based on verifiable metrics
- **Collaboration Tracking**: Monitor institutional research networks
- **Quality Assurance**: Maintain academic integrity standards

### Research Communities
- **Network Analysis**: Analyze citation patterns and research trends
- **Impact Assessment**: Evaluate research impact across disciplines
- **Collaboration Discovery**: Identify potential research collaborators
- **Trend Identification**: Track emerging research areas and methodologies

## Error Handling

The contract includes comprehensive error handling:
- `ERR-UNAUTHORIZED-ACCESS` (100): Insufficient permissions
- `ERR-DUPLICATE-RESOURCE` (101): Resource already exists
- `ERR-RESOURCE-NOT-FOUND` (102): Requested resource not found
- `ERR-SELF-CITATION-FORBIDDEN` (103): Self-citation attempt
- `ERR-INVALID-PARAMETER` (104): Invalid parameter value
- `ERR-MALFORMED-INPUT` (105): Improperly formatted input
- `ERR-INSUFFICIENT-BALANCE` (106): Insufficient token balance