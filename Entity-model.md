# Canonical Entity Model: Payment Failure Event
**Domain:** BFSI / Real-time Payments  
**Status:** Production Validated  

## 1. Overview
This model defines the unified structure for payment failure events across three disparate payment gateways (GW-A, GW-B, and Legacy-C). Before this model, the failure reasons were non-standardized, preventing real-time automated recovery.

## 2. Attributes (12 Core Fields)

| Attribute Name | Data Type | Requirement | Description | Sample Value |
| :--- | :--- | :--- | :--- | :--- |
| `failure_id` | UUID | Mandatory | Unique ID for the failure event. | `f0e4c2...` |
| `original_txn_id` | String | Mandatory | The ID of the transaction that failed. | `TXN_99821` |
| `source_system` | Enum | Mandatory | Originating gateway (e.g., GW_A, GW_B). | `GW_A` |
| `canonical_category` | String | Mandatory | **Governed Value** (see Taxonomy section). | `CONNECTION_ISSUE` |
| `raw_error_code` | String | Optional | The unmapped code returned by the API. | `TIMEOUT_01` |
| `is_retryable` | Boolean | Mandatory | Flag indicating if STP is possible. | `true` |
| `failure_timestamp` | ISO-8601 | Mandatory | Event time in UTC. | `2024-05-14T12:00:00Z` |
| `currency` | String | Mandatory | ISO-4217 Currency code. | `GBP` |

## 3. The 8 Canonical Categories (Taxonomy)
These categories were derived through affinity mapping of 50+ raw error codes.

1. **CONNECTION_ISSUE**: Network timeouts or gateway unreachable.
2. **INSUFFICIENT_FUNDS**: Customer-side balance issues.
3. **AUTH_FAILURE**: Invalid credentials or MFA failure.
4. **COMPLIANCE_REJECT**: AML or Sanctions screening hits.
5. **VELOCITY_LIMIT**: Fraud-prevention triggers (too many txns).
6. **FORMAT_ERROR**: Missing mandatory fields in payload.
7. **DOWNSTREAM_OFFLINE**: Bank partner API is down.
8. **UNKNOWN**: Unmapped codes (requires manual stewardship).

## 4. Design Rationale
* **Abstraction over Accuracy:** We prioritize the `canonical_category` for business reporting, while retaining `raw_error_code` for technical forensics.
* **STP Alignment:** The `is_retryable` flag is derived from the category mapping to drive the **81% Straight Through Processing** rate.
