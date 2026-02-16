# Secure Infrastructure Observability (Forwarders + Aggregation + Retention)

![Security](https://img.shields.io/badge/focus-Observability%20%26%20SIEM-blue)
![Architecture](https://img.shields.io/badge/deliverable-Architecture%20Docs-success)
![Ops](https://img.shields.io/badge/ops-Runbooks%20%2F%20SOPs-informational)

A practical observability + security telemetry project showing how to design:
- Log collection from endpoints/servers
- Forwarders + aggregation pipeline
- Normalization and enrichment
- Secure retention and access controls
- Operational runbooks and troubleshooting steps

This repo is intentionally documentation-heavy to mirror real SIEM engineering work.

---

## Table of Contents
- [What You’ll Build](#what-youll-build)
- [Reference Architecture](#reference-architecture)
- [Threat Model (Lite)](#threat-model-lite)
- [Prerequisites](#prerequisites)
- [Repo Structure](#repo-structure)
- [Step 1 — Define Log Sources](#step-1--define-log-sources)
- [Step 2 — Collection & Forwarding Design](#step-2--collection--forwarding-design)
- [Step 3 — Normalization & Enrichment](#step-3--normalization--enrichment)
- [Step 4 — Retention, Security, and Access](#step-4--retention-security-and-access)
- [Step 5 — Operational Runbooks](#step-5--operational-runbooks)
- [Step 6 — Validation Checklist](#step-6--validation-checklist)
- [Troubleshooting](#troubleshooting)
- [Resources](#resources)
- [License](#license)

---

## What You’ll Build
Deliverables suitable for interviews and portfolios:
- Architecture diagram of an observability pipeline
- Log source inventory + event taxonomy
- Retention policy template and security controls
- Runbooks for on-call troubleshooting
- Validation checklist for go-live

---

## Reference Architecture

```mermaid
flowchart TB
  subgraph Sources
    W[Windows Servers/Workstations]
    L[Linux Servers]
    N[Network Devices]
    C[Cloud Logs]
  end

  subgraph Collection
    F1[Forwarders/Collectors]
    F2[Syslog/Agent]
  end

  subgraph Aggregation
    A[Aggregator<br/>Queue/Buffer/Transform]
  end

  subgraph Storage
    S[(SIEM / Data Lake)]
  end

  subgraph Consumers
    D[Detections]
    H[Hunters]
    IR[Incident Response]
    R[Reports]
  end

  W --> F1 --> A --> S
  L --> F2 --> A --> S
  N --> F2 --> A --> S
  C --> A --> S

  S --> D
  S --> H
  S --> IR
  S --> R
