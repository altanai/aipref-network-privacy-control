---
title: "AI Preferences for Privacy-Preserving Network Traffic Analysis"
abbrev: "AI Network Privacy Control"
category: std
docname: draft-aipref-network-privacy-control-00-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: "Web and Internet Transport"
workgroup: "AI Preferences"
keyword:
 - AI preferences
 - network privacy
 - traffic analysis
 - leak detection
venue:
  group: "AI Preferences"
  type: "Working Group"
  mail: "ai-control@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/ai-control/"
  github: "ietf-wg-aipref"
  latest: "https://ietf-wg-aipref.github.io/"

author:
 -
    fullname: "Altanai Bisht"
    organization: "Cisco"
    email: "altanai@outlook.com"

normative:
  RFC2119:
  RFC8174:
  RFC8615:
  RFC9309:

informative:
  RFC6973:
  RFC7258:
  RFC8446:

--- abstract

This document defines a framework for expressing and enforcing preferences about how Artificial Intelligence (AI) agents collect, process, and analyze network traffic data for the purposes of detecting network anomalies, unfair usage patterns, and implementing intelligent network control. The framework enables network operators and users to specify granular preferences regarding what traffic characteristics may be exposed to AI systems while maintaining privacy guarantees and preventing sensitive information leakage.

This work extends the AI Preferences vocabulary to the domain of network traffic analysis, providing mechanisms for reconciling competing privacy requirements with the operational need for intelligent network monitoring and control.

--- middle

# Introduction

## Motivation

The increasing deployment of AI-based systems for network monitoring, traffic analysis, and intelligent control presents significant opportunities for improved network performance, security, and resource allocation. However, these systems also raise substantial privacy concerns when they process traffic metadata and patterns that may reveal sensitive information about users, organizations, and network behavior.

Network operators need to detect and respond to:
- Unfair usage patterns and bandwidth abuse
- Network anomalies and potential security threats  
- Performance degradation and congestion
- Protocol violations and malicious traffic

Simultaneously, users and organizations require:
- Privacy protection for their traffic patterns
- Control over what network characteristics are exposed to AI systems
- Guarantees about data retention and processing
- Transparency about AI-based monitoring activities

This document addresses the challenge of enabling AI-driven network intelligence while respecting privacy preferences through standardized preference expression and enforcement mechanisms.

## Scope

This document defines:

1. A vocabulary for expressing preferences about AI processing of network traffic data
2. Mechanisms for attaching these preferences to network flows and traffic metadata
3. Methods for AI agents to discover and respect these preferences
4. A framework for reconciling conflicting preferences from multiple stakeholders
5. Privacy-preserving techniques for network traffic analysis

This document does NOT address:

- Technical enforcement mechanisms for preventing preference violations
- Authentication and authorization of AI agents or monitoring systems
- Specific AI/ML algorithms for traffic analysis
- Network-layer security protocols
- Legal or regulatory compliance requirements

## Requirements Language

{::boilerplate bcp14-tagged}

# Problem Statement

## Current Challenges

### Uncontrolled AI Access to Network Data

Current network monitoring systems often have unrestricted access to traffic metadata including:
- Source and destination IP addresses and ports
- Packet timing and sizes
- Protocol types and patterns
- Flow durations and volumes
- Application layer indicators

AI systems processing this data can infer sensitive information such as:
- User behavior patterns and activities
- Organizational structure and communication patterns
- Geographic locations and movements
- Application usage and content types
- Business relationships and partnerships

### Lack of Standardized Preference Expression

There is no standardized mechanism for:
- Network administrators to express what data AI systems may access
- Users to specify privacy requirements for their traffic
- Organizations to communicate data processing policies
- AI agents to discover and understand these preferences
- Reconciling preferences across different stakeholders

### Privacy vs. Functionality Trade-offs

Network operators face difficult choices between:
- Detecting unfair usage vs. respecting user privacy
- Implementing intelligent QoS vs. exposing traffic patterns
- Identifying security threats vs. revealing network topology
- Optimizing performance vs. protecting business confidentiality

## Use Cases

### Use Case 1: Detecting Unfair Bandwidth Usage

A network operator wants to use AI to detect users consuming disproportionate bandwidth or violating fair usage policies, but must:
- Not expose individual user identities to the AI system
- Not reveal specific applications or content being accessed
- Only provide aggregate traffic statistics at appropriate granularity
- Limit retention of detailed flow records

**Preference Expression Needed:**
```
AI-Processing-Scope: aggregate-flows
AI-Temporal-Granularity: 5min-buckets
AI-Identity-Level: anonymized
AI-Retention-Period: 24h
AI-Allowed-Features: volume, packet-rate, flow-count
AI-Forbidden-Features: payload, endpoints, timing-precision
```

### Use Case 2: DDoS Detection Without Privacy Leakage

A security AI agent monitors for distributed denial of service attacks while preserving privacy:
- Analyzes traffic patterns for anomalous behavior
- Does not track individual legitimate user sessions
- Aggregates statistics to prevent identification
- Triggers alerts without exposing traffic content

**Preference Expression Needed:**
```
AI-Processing-Purpose: ddos-detection
AI-Identity-Level: pseudonymized
AI-Aggregation-Level: per-prefix-24
AI-Feature-Access: packet-rates, syn-ratios, geographic-distribution
AI-Alert-Detail-Level: aggregate-only
AI-Audit-Required: true
```

### Use Case 3: Intelligent Traffic Engineering

An AI system optimizes routing and load balancing while respecting organizational privacy:
- Analyzes traffic matrices and flow patterns
- Does not expose individual customer traffic
- Aggregates flows by destination prefix
- Provides recommendations without accessing sensitive attributes

**Preference Expression Needed:**
```
AI-Processing-Purpose: traffic-engineering
AI-Flow-Granularity: per-prefix-aggregate
AI-Temporal-Resolution: 1h
AI-Exposed-Metrics: volume, destination-prefix, qos-class
AI-Protected-Metrics: source-identity, application-type, payload-size-distribution
AI-Processing-Location: on-premises
```

### Use Case 4: Multi-Tenant Network Privacy

In a multi-tenant environment, different organizations have varying privacy requirements:
- Tenant A allows detailed traffic analysis for security
- Tenant B requires minimal AI processing with strong anonymization
- Tenant C prohibits any AI processing of their traffic
- The system must reconcile and enforce these preferences

**Preference Reconciliation Needed:**
```
Tenant-A: AI-Processing: permitted, AI-Detail-Level: high
Tenant-B: AI-Processing: limited, AI-Anonymization: required
Tenant-C: AI-Processing: prohibited
Resolution: per-tenant enforcement with strictest-wins policy
```

# Architecture

## Components

### Preference Originators

Entities that express preferences about AI processing:
- Network administrators and operators
- End users and subscriber organizations  
- Equipment vendors and service providers
- Regulatory authorities and policies

### Preference Attachers

Mechanisms for associating preferences with network traffic:
- Flow metadata tags and attributes
- Router/switch configuration directives
- Protocol signaling (e.g., IP options, extension headers)
- Out-of-band policy distribution systems

### AI Processing Agents

Systems that consume network data and respect preferences:
- Traffic analysis and monitoring systems
- Anomaly detection engines
- Intelligent control plane systems
- Network optimization algorithms

### Preference Enforcement Points

Components that enforce preference compliance:
- Flow collectors with preference-aware filtering
- AI agent authorization and access control systems
- Audit and compliance monitoring systems
- Privacy-preserving data transformation proxies

## Information Flow

```
┌─────────────────┐
│ Preference      │
│ Originators     │
└────────┬────────┘
         │ Express preferences
         ▼
┌─────────────────────────────────────────┐
│ Preference Storage & Distribution       │
│ - Policy repositories                   │
│ - Configuration management              │
│ - Protocol signaling                    │
└────────┬────────────────────────────────┘
         │ Attach/signal preferences
         ▼
┌─────────────────────────────────────────┐
│ Network Traffic Flows                   │
│ - Packet streams                        │
│ - Flow records                          │
│ - Metadata                              │
└────────┬────────────────────────────────┘
         │ 
         ▼
┌─────────────────────────────────────────┐
│ Preference Enforcement Points           │
│ - Filter/transform based on preferences │
│ - Apply privacy-preserving techniques   │
│ - Audit access                          │
└────────┬────────────────────────────────┘
         │ Preference-filtered data
         ▼
┌─────────────────────────────────────────┐
│ AI Processing Agents                    │
│ - Respect preferences                   │
│ - Process within constraints            │
│ - Report compliance                     │
└─────────────────────────────────────────┘
```

# Preference Vocabulary

## Core Preference Categories

### Processing Scope Preferences

Define what aspects of network traffic AI agents may access:

- **AI-Processing-Scope**: Controls the level of traffic data access
  - Values: `none`, `metadata-only`, `aggregate-flows`, `individual-flows`, `full-access`
  
- **AI-Processing-Purpose**: Restricts processing to specific purposes
  - Values: `leak-detection`, `ddos-protection`, `traffic-engineering`, `qos-optimization`, `security-monitoring`, `performance-analysis`

### Identity Protection Preferences

Control how identity information is handled:

- **AI-Identity-Level**: Specifies identity exposure requirements
  - Values: `identified`, `pseudonymized`, `anonymized`, `aggregated`, `no-identity`

- **AI-Identity-Scope**: Defines what constitutes identity in context
  - Values: `ip-address`, `user-id`, `device-id`, `session-id`, `flow-id`

### Temporal Preferences

Control time-based aspects of data processing:

- **AI-Temporal-Granularity**: Minimum time aggregation window
  - Values: time duration (e.g., `1min`, `5min`, `1h`, `1d`)

- **AI-Retention-Period**: Maximum data retention duration
  - Values: time duration (e.g., `1h`, `24h`, `7d`, `30d`, `none`)

- **AI-Retention-Detail**: Specifies detail level over time
  - Values: `full:1h,aggregate:24h,summary:7d` (multi-tier retention)

### Feature Access Preferences

Control what traffic characteristics may be processed:

- **AI-Allowed-Features**: Explicitly permitted traffic features
  - Values: comma-separated list from feature taxonomy

- **AI-Forbidden-Features**: Explicitly prohibited traffic features
  - Values: comma-separated list from feature taxonomy

- **AI-Feature-Aggregation**: Required aggregation for features
  - Values: `none`, `statistical-only`, `histogram`, `quantiles`

### Processing Location Preferences

Control where AI processing occurs:

- **AI-Processing-Location**: Required processing location
  - Values: `on-premises`, `trusted-cloud`, `same-jurisdiction`, `any`

- **AI-Data-Export**: Controls data export for processing
  - Values: `prohibited`, `aggregated-only`, `anonymized-only`, `permitted`

### Audit and Transparency Preferences

Control monitoring and accountability:

- **AI-Audit-Required**: Whether audit logging is required
  - Values: `true`, `false`

- **AI-Transparency-Level**: Required disclosure about AI processing
  - Values: `none`, `purpose-only`, `detailed`, `full`

- **AI-Access-Notification**: Whether access should trigger notifications
  - Values: `none`, `summary`, `real-time`

## Feature Taxonomy

Network traffic features that may be subject to preferences:

### Layer 3/4 Features
- `src-ip`, `dst-ip`, `src-port`, `dst-port`
- `protocol`, `ttl`, `ip-flags`
- `packet-size`, `packet-rate`
- `flow-duration`, `flow-volume`

### Aggregate Features
- `flow-count`, `connection-rate`
- `bandwidth-usage`, `traffic-volume`
- `protocol-distribution`, `port-distribution`

### Temporal Features
- `inter-arrival-time`, `burst-patterns`
- `time-of-day-patterns`, `periodicity`

### Statistical Features  
- `packet-size-distribution`, `flow-size-distribution`
- `traffic-entropy`, `pattern-regularity`

### Derived Features
- `application-signature`, `behavior-pattern`
- `anomaly-score`, `similarity-metric`

# Preference Attachment Mechanisms

## In-Band Signaling

### IPv6 Destination Options Header

AI preferences can be signaled using IPv6 extension headers:

```
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Next Header  |  Hdr Ext Len  |  Option Type  | Opt Data Len  |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    AI Preference Token                        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

Option Type: TBD (to be assigned by IANA)
Option Data: Compact preference token or URI reference

### Flow Metadata Export

Preferences attached to flow records (e.g., IPFIX/NetFlow):

```
Information Element: aiPreferencePolicy
ElementId: TBD
Type: string
Description: URI or token referencing AI preference policy
```

## Out-of-Band Mechanisms

### Well-Known URI for Network Preferences

Similar to robots.txt, define a well-known URI for network AI preferences:

```
https://network.example.com/.well-known/ai-network-preferences
```

Content format:
```
User-agent: *
Processing-scope: aggregate-flows
Identity-level: anonymized
Retention-period: 24h
Allowed-purposes: leak-detection, ddos-protection
Forbidden-features: payload, timing-precision

User-agent: TrustedMonitor
Processing-scope: individual-flows
Identity-level: pseudonymized  
Retention-period: 7d
```

### DNS TXT Records

AI preferences published via DNS:

```
_aipref.example.com. IN TXT "v=aipref1; scope=aggregate; identity=anon; retention=24h"
```

### YANG Data Models

For network management systems, define YANG models:

```yang
module ietf-ai-network-preferences {
  namespace "urn:ietf:params:xml:ns:yang:ietf-ai-network-preferences";
  prefix "aipref";
  
  container ai-preferences {
    leaf processing-scope {
      type enumeration {
        enum none;
        enum metadata-only;
        enum aggregate-flows;
        enum individual-flows;
      }
    }
    
    leaf identity-level {
      type enumeration {
        enum identified;
        enum pseudonymized;
        enum anonymized;
      }
    }
    
    leaf retention-period {
      type uint32;
      units "seconds";
    }
    
    leaf-list allowed-purposes {
      type string;
    }
  }
}
```

## Preference Discovery

AI agents MUST discover preferences through this precedence order:

1. **In-band signaling**: Flow-level preferences in packet headers or flow metadata (highest precedence)
2. **Network-level policy**: Configured preferences on network equipment
3. **DNS-based discovery**: Published preferences via DNS TXT records
4. **Well-known URI**: HTTP-accessible preference documents
5. **Default policy**: Conservative defaults when no preferences found (lowest precedence)

# Preference Reconciliation

## Multiple Preference Sources

When multiple preferences apply, use the following reconciliation rules:

### Strictest-Wins Policy

For conflicting privacy preferences, the strictest/most privacy-preserving MUST be applied:

```
Preference A: AI-Identity-Level: pseudonymized
Preference B: AI-Identity-Level: anonymized
Result: AI-Identity-Level: anonymized (stricter)
```

```
Preference A: AI-Retention-Period: 7d
Preference B: AI-Retention-Period: 24h  
Result: AI-Retention-Period: 24h (stricter)
```

### Intersection for Allowed Features

When multiple preferences specify allowed features, use intersection:

```
Preference A: AI-Allowed-Features: volume, packet-rate, flow-count
Preference B: AI-Allowed-Features: volume, flow-count, protocol
Result: AI-Allowed-Features: volume, flow-count (intersection)
```

### Union for Forbidden Features

When multiple preferences specify forbidden features, use union:

```
Preference A: AI-Forbidden-Features: payload, src-ip
Preference B: AI-Forbidden-Features: dst-ip, timing-precision
Result: AI-Forbidden-Features: payload, src-ip, dst-ip, timing-precision
```

### Purpose Intersection

Processing is only permitted for purposes allowed by all applicable preferences:

```
Preference A: AI-Allowed-Purposes: leak-detection, ddos-protection, qos
Preference B: AI-Allowed-Purposes: ddos-protection, qos, security-monitoring
Result: AI-Allowed-Purposes: ddos-protection, qos
```

## Conflict Resolution Algorithm

```
Algorithm: Reconcile-AI-Preferences(preferences[])
  
  result = new AIPreferenceSet()
  
  // Processing scope - strictest wins
  result.scope = min(preferences.map(p => p.scope))
  
  // Identity level - strictest wins  
  result.identity = strictest(preferences.map(p => p.identity))
  
  // Retention period - shortest wins
  result.retention = min(preferences.map(p => p.retention))
  
  // Allowed features - intersection
  result.allowed_features = intersect(preferences.map(p => p.allowed_features))
  
  // Forbidden features - union
  result.forbidden_features = union(preferences.map(p => p.forbidden_features))
  
  // Allowed purposes - intersection
  result.allowed_purposes = intersect(preferences.map(p => p.allowed_purposes))
  
  // Location constraints - strictest wins
  result.location = strictest(preferences.map(p => p.location))
  
  // Audit requirements - any true makes result true
  result.audit_required = any(preferences.map(p => p.audit_required))
  
  return result
```

# Privacy-Preserving Techniques

## Data Minimization

AI agents SHOULD use privacy-preserving techniques to minimize data exposure:

### K-Anonymity for Flow Records

Ensure that flow records cannot be linked to fewer than k individual sources:

```
Original flows:
  192.168.1.5 -> 10.0.0.1 (100MB)
  192.168.1.8 -> 10.0.0.1 (150MB)
  
K-anonymized (k=10):
  192.168.1.0/28 -> 10.0.0.0/24 (2.5GB, 10 sources)
```

### Differential Privacy for Statistics

Add calibrated noise to aggregate statistics:

```
True bandwidth usage by prefix: 1.5 Gbps
Reported with ε=0.1 differential privacy: 1.53 Gbps
```

### Temporal Aggregation

Aggregate traffic over time windows to prevent timing attacks:

```
Original: per-packet timestamps
Privacy-preserving: 5-minute volume aggregates
```

### Feature Suppression

Remove features that enable inference of sensitive attributes:

```
Full feature set: [volume, packet_rate, port_dist, size_dist, timing_pattern]
Suppressed: [volume, packet_rate]  // Remove timing/size that reveal application
```

## Pseudonymization and Anonymization

### Consistent Pseudonyms

Use cryptographic hashing with rotation for pseudonyms:

```
pseudonym = HMAC-SHA256(key_of_day, real_identifier)
```

Rotation period specified by `AI-Retention-Period` preference.

### IP Address Anonymization

Apply prefix-preserving anonymization:

```
Original: 192.168.1.5
Anonymized: 10.200.45.78 (preserves /24 boundaries)
```

## Secure Multi-Party Computation

For multi-stakeholder scenarios, use secure computation:

```
Party A: Has flow records
Party B: Has anomaly detection model
Goal: Detect anomalies without A revealing flows or B revealing model

Solution: MPC protocol where:
  - A learns only: anomaly/normal classification
  - B learns only: aggregate statistics
  - Neither learns other's private data
```

# Security Considerations

## Preference Integrity

Preferences MUST be protected against tampering:

- Use cryptographic signatures for preference documents
- Authenticate preference sources using existing mechanisms (DNSSEC, TLS)
- Validate preference tokens before applying
- Audit preference changes and access

## Preference Confidentiality

Some preferences may themselves be sensitive:

- Encrypt preference transmission where appropriate
- Consider privacy implications of preference disclosure
- Allow private preference channels for sensitive policies

## Enforcement Limitations

This specification defines preference expression, not technical enforcement:

- Preferences are advisory, not mandatory enforcement mechanisms
- AI agents MUST respect preferences but malicious agents could ignore them
- Audit and compliance monitoring are essential
- Legal and contractual mechanisms may be necessary for enforcement

## Privacy Attacks

### Inference Attacks

Even aggregated/anonymized data may enable inference:

- Use differential privacy with appropriate privacy budgets
- Implement minimum aggregation thresholds (k-anonymity)
- Rotate pseudonyms regularly
- Monitor for correlation attacks across data releases

### Timing Attacks

Traffic timing can reveal sensitive information:

- Aggregate temporal data per preferences
- Add random delays or buffering where appropriate
- Suppress high-resolution timing features

### Fingerprinting

Combinations of features may uniquely identify users/flows:

- Limit feature combinations available to AI agents
- Use generalization and suppression techniques
- Monitor for rare combinations that enable identification

## Denial of Service

Preference processing must not enable DoS:

- Limit preference document size and complexity
- Cache and validate preferences
- Rate-limit preference lookups
- Use default conservative policies when discovery fails

# IANA Considerations

## IPv6 Destination Options

IANA is requested to assign a new IPv6 Destination Option Type:

```
Option Type: TBD
Description: AI Processing Preferences
Reference: This document
```

## Well-Known URI

IANA is requested to register a new well-known URI:

```
URI suffix: ai-network-preferences
Change controller: IETF
Specification document: This document
Status: permanent
```

## IPFIX Information Elements

IANA is requested to assign new IPFIX Information Elements:

```
ElementId: TBD1
Name: aiPreferencePolicy
Data Type: string
Description: URI or token referencing AI preference policy
Reference: This document

ElementId: TBD2  
Name: aiProcessingScope
Data Type: unsigned8
Description: Allowed scope of AI processing
Reference: This document

ElementId: TBD3
Name: aiIdentityLevel  
Data Type: unsigned8
Description: Required identity protection level
Reference: This document
```

## AI Preference Parameters Registry

IANA is requested to create a new registry: "AI Network Preference Parameters"

Initial entries:

```
Parameter Name: AI-Processing-Scope
Allowed Values: none, metadata-only, aggregate-flows, individual-flows, full-access
Reference: This document

Parameter Name: AI-Identity-Level
Allowed Values: identified, pseudonymized, anonymized, aggregated, no-identity  
Reference: This document

Parameter Name: AI-Processing-Purpose
Allowed Values: leak-detection, ddos-protection, traffic-engineering, qos-optimization, 
                security-monitoring, performance-analysis
Reference: This document

[Additional parameters as defined in Section 5]
```

Registration procedure: Specification Required (RFC 8126)

## Network Traffic Feature Registry

IANA is requested to create a new registry: "AI Network Traffic Features"

Initial entries as defined in Section 5.2.

Registration procedure: Expert Review (RFC 8126)

# Implementation Considerations

## AI Agent Implementation

AI agents SHOULD:

1. **Discover preferences** using all available mechanisms
2. **Reconcile preferences** using the algorithm in Section 6.2
3. **Filter data** before processing to match preferences
4. **Apply privacy techniques** (aggregation, anonymization) as required
5. **Log access** if audit is required
6. **Fail closed** if preferences cannot be determined

Example implementation flow:

```python
def process_network_traffic(flow_data, ai_agent_id):
    # 1. Discover preferences
    prefs = discover_preferences(flow_data.source_network)
    
    # 2. Reconcile if multiple sources
    effective_prefs = reconcile_preferences(prefs)
    
    # 3. Check if processing is allowed
    if not can_process(ai_agent_id, effective_prefs):
        return None  # Processing not permitted
    
    # 4. Filter and transform data
    filtered_data = apply_preference_filters(flow_data, effective_prefs)
    
    # 5. Apply privacy-preserving techniques
    private_data = apply_privacy_transforms(filtered_data, effective_prefs)
    
    # 6. Audit if required
    if effective_prefs.audit_required:
        log_access(ai_agent_id, flow_data.source, effective_prefs)
    
    # 7. Process with AI
    return ai_agent.analyze(private_data)
```

## Network Equipment Implementation

Network devices (routers, switches, flow collectors) SHOULD:

1. **Accept preference configuration** from administrators
2. **Attach preferences** to flow metadata (IPFIX/NetFlow)
3. **Enforce basic filtering** before export
4. **Support preference signaling** in packet headers (IPv6 options)
5. **Publish preferences** via DNS or well-known URIs

## Deployment Strategies

### Incremental Deployment

Start with coarse-grained preferences and refine over time:

Phase 1: Network-wide default policy
Phase 2: Per-tenant or per-prefix policies  
Phase 3: Per-flow signaling for critical traffic
Phase 4: Dynamic preference negotiation

### Backwards Compatibility

For equipment that doesn't support AI preferences:

- Use conservative default policies
- Deploy preference enforcement proxies
- Leverage existing privacy mechanisms (ACLs, sampling)
- Monitor and audit access

# Examples

## Example 1: ISP Fair Usage Monitoring

An ISP wants to detect customers violating fair usage policies while protecting privacy:

**Preference Configuration:**
```
AI-Processing-Purpose: leak-detection
AI-Processing-Scope: aggregate-flows
AI-Temporal-Granularity: 5min
AI-Identity-Level: pseudonymized
AI-Retention-Period: 24h
AI-Allowed-Features: volume, flow-count, protocol-distribution
AI-Forbidden-Features: dst-ip, payload, timing-precision
AI-Aggregation-Level: per-customer
```

**AI Agent Behavior:**
- Receives 5-minute aggregate volumes per customer pseudonym
- Analyzes for outliers (>95th percentile sustained)
- Cannot identify specific destinations or applications
- Cannot track individual flows
- Data deleted after 24 hours

**Privacy Protection:**
- Customer identity pseudonymized (rotated daily)
- No access to traffic content or specific destinations
- Only aggregate statistics available
- Short retention period limits exposure

## Example 2: DDoS Detection in Multi-Tenant Data Center

Data center operator protects against DDoS while respecting tenant preferences:

**Tenant A (Relaxed) Preferences:**
```
AI-Processing-Purpose: ddos-protection
AI-Processing-Scope: individual-flows
AI-Identity-Level: pseudonymized
AI-Allowed-Features: src-ip, dst-ip, packet-rate, protocol
```

**Tenant B (Strict) Preferences:**
```
AI-Processing-Purpose: ddos-protection
AI-Processing-Scope: aggregate-flows
AI-Identity-Level: anonymized  
AI-Allowed-Features: packet-rate, flow-count
AI-Forbidden-Features: src-ip, dst-ip
```

**Reconciled for Shared Infrastructure:**
```
AI-Processing-Purpose: ddos-protection
AI-Processing-Scope: aggregate-flows (stricter)
AI-Identity-Level: anonymized (stricter)
AI-Allowed-Features: packet-rate, flow-count (intersection)
AI-Forbidden-Features: src-ip, dst-ip (union from Tenant B)
```

**AI Agent Behavior:**
- Monitors aggregate packet rates and connection counts
- Detects anomalous patterns without individual flow tracking
- Triggers mitigation based on aggregate statistics
- Cannot attribute specific traffic to individual tenants

## Example 3: Enterprise Network with Regulatory Requirements

Enterprise in regulated industry (healthcare/finance) with strict privacy requirements:

**Preference Configuration:**
```
AI-Processing-Purpose: security-monitoring, performance-analysis
AI-Processing-Scope: metadata-only
AI-Identity-Level: no-identity
AI-Retention-Period: 1h
AI-Allowed-Features: volume, protocol, flow-count
AI-Forbidden-Features: ip-addresses, timing-precision, payload
AI-Processing-Location: on-premises
AI-Data-Export: prohibited
AI-Audit-Required: true
AI-Transparency-Level: full
```

**AI Agent Behavior:**
- Processes only aggregate traffic volumes and protocol distribution
- No access to identity information (IPs suppressed)
- All processing occurs on-premises
- Cannot export data to cloud services
- All access logged for compliance audit
- Provides full transparency reports

**Privacy Protection:**
- Cannot correlate traffic to individuals or departments
- Short retention prevents long-term pattern analysis  
- On-premises processing prevents data exposure
- Audit trail for regulatory compliance

# Operational Considerations

## Monitoring and Compliance

Operators SHOULD:

- Monitor AI agent compliance with preferences
- Log preference violations and access patterns
- Generate periodic compliance reports
- Alert on unexpected data access

## Performance Impact

Preference enforcement may impact performance:

- Preference discovery adds latency (mitigate with caching)
- Data filtering/transformation adds processing overhead
- Privacy-preserving techniques (DP, MPC) can be expensive
- Balance privacy requirements with operational needs

## Preference Management

Organizations should establish processes for:

- Defining and updating preferences
- Reconciling stakeholder requirements
- Testing preference effectiveness
- Responding to privacy incidents
- Reviewing and auditing AI access

--- back

# Acknowledgments

This document builds on the foundational work of the IETF AI Preferences Working Group and incorporates concepts from privacy-preserving network monitoring research.

# Appendix A: Privacy-Preserving Traffic Analysis Techniques

## A.1 Differential Privacy Mechanisms

Laplace mechanism for count queries:
```
ε = privacy budget
Δf = sensitivity of query (typically 1 for counts)
noise ~ Laplace(Δf/ε)
noisy_result = true_result + noise
```

## A.2 K-Anonymity Generalization

IP address generalization hierarchy:
```
Level 0: 192.168.1.5 (full address)
Level 1: 192.168.1.0/24 (subnet)
Level 2: 192.168.0.0/16 (larger subnet)
Level 3: 192.0.0.0/8 (class A)
```

## A.3 Secure Aggregation Protocols

Multi-party secure sum for distributed statistics:
```
Parties: P1, P2, ..., Pn each with private value vi
Goal: Compute sum Σvi without revealing individual values

Protocol:
1. Each Pi generates random shares: vi = si1 + si2 + ... + sin
2. Pi sends sij to Pj (encrypted)
3. Each Pj computes partial_sum_j = Σi sij  
4. All parties combine partial sums to get total
```

# Appendix B: Example Preference Documents

## B.1 ISP Fair Usage Policy
```json
{
  "version": "aipref-network-1.0",
  "scope": "network:203.0.113.0/24",
  "preferences": {
    "processing-purpose": ["leak-detection", "ddos-protection"],
    "processing-scope": "aggregate-flows",
    "identity-level": "pseudonymized",
    "temporal-granularity": "5min",
    "retention-period": "24h",
    "allowed-features": [
      "volume", "flow-count", "protocol-distribution"
    ],
    "forbidden-features": [
      "dst-ip", "payload", "timing-precision"
    ],
    "audit-required": true
  }
}
```

## B.2 Enterprise Security Monitoring
```json
{
  "version": "aipref-network-1.0",
  "scope": "network:10.0.0.0/8",
  "preferences": {
    "processing-purpose": ["security-monitoring"],
    "processing-scope": "metadata-only",
    "identity-level": "anonymized",
    "retention-period": "1h",
    "processing-location": "on-premises",
    "data-export": "prohibited",
    "allowed-features": [
      "volume", "protocol", "flow-count"
    ],
    "forbidden-features": [
      "ip-addresses", "port-numbers", "timing-precision", "payload"
    ],
    "audit-required": true,
    "transparency-level": "full"
  }
}
```

## B.3 Research Network with Consent
```json
{
  "version": "aipref-network-1.0",
  "scope": "network:198.51.100.0/24",
  "preferences": {
    "processing-purpose": ["research", "performance-analysis"],
    "processing-scope": "individual-flows",
    "identity-level": "pseudonymized",
    "retention-period": "30d",
    "allowed-features": [
      "volume", "packet-rate", "flow-duration", 
      "protocol", "packet-size-distribution"
    ],
    "consent-obtained": true,
    "audit-required": true,
    "data-minimization-required": false
  }
}
```

# Appendix C: AI Agent Compliance Checklist

AI agents processing network traffic SHOULD verify:

- [ ] Preference discovery attempted via all supported mechanisms
- [ ] Preferences reconciled correctly when multiple sources exist
- [ ] Processing purpose matches allowed purposes
- [ ] Processing scope does not exceed preference limits
- [ ] Identity protection level meets or exceeds requirements
- [ ] Only allowed features are accessed/processed
- [ ] Forbidden features are filtered/suppressed
- [ ] Temporal aggregation applied per preferences
- [ ] Data retention does not exceed specified period
- [ ] Processing location constraints satisfied
- [ ] Audit logging enabled if required
- [ ] Privacy-preserving techniques applied appropriately
- [ ] Compliance monitoring active
- [ ] Default-deny policy applied when preferences unclear

---

