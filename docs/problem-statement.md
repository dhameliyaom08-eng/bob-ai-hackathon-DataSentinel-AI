# Problem Statement

## Background

Modern enterprises depend on interconnected data pipelines that move information across APIs, databases, ETL/ELT processes, data warehouses, analytics dashboards, and machine-learning systems. A single customer record, transaction, or business event can therefore pass through multiple processing stages before reaching the final system where it is consumed.

This architecture creates a significant operational challenge: a data-quality problem may originate at an upstream source but only become visible several steps later as an incorrect dashboard value, abnormal metric, failed transformation, or degraded machine-learning input.

Data teams therefore need more than simple monitoring. They need to understand what went wrong, where it most likely started, what systems were affected, and what should be addressed first.

## The Problem

Enterprise data-quality tools commonly identify symptoms such as abnormal null rates, duplicate records, schema changes, or statistical drift. However, detecting an anomaly is only the beginning of an incident investigation.

When an incident occurs, engineers may need to manually correlate:

data-quality metrics
pipeline execution logs
schema changes
timestamps
upstream and downstream dependencies
lineage information
business-critical consumers

The result is a fragmented investigation process that has to be reconstructed for each incident.

## Who is Affected

Primary users

Data Engineers

Data engineers are responsible for pipelines and data transformations and are often among the first people involved when a pipeline or data-quality check fails. They need to quickly determine which dataset or process is responsible, when the issue began, and what upstream evidence is relevant.

Data Platform / Data Reliability Engineers

These engineers are responsible for the reliability of data platforms and need to understand the full downstream impact of an incident. Their key question is whether other datasets, pipelines, dashboards, or models are currently being affected.

Analytics Engineers

Analytics engineers may discover that a business dashboard or report contains unexpected results without owning the upstream pipeline that produced the data. They need a clear explanation of whether the issue is caused by a data incident and where responsibility for the problem may lie.

ML Platform Engineers

Machine-learning teams may encounter feature drift or abnormal model inputs and need to determine whether the change reflects genuine business behavior or corruption introduced earlier in the data pipeline.

## Why It Matters

The main cost of a data-quality incident is not necessarily the initial anomaly itself. The larger problem is the time and uncertainty involved in determining its source, impact, and priority.

A relatively small issue in a low-importance staging dataset may require very different action from a similar anomaly affecting a revenue-critical dashboard or a machine-learning pipeline.

Without impact context, two technically similar alerts can have very different business consequences. DataSentinel therefore evaluates not only the magnitude of an anomaly but also factors such as:

number of records affected
dataset criticality
number of downstream systems reached
duration of the incident
confidence in the identified source

This allows the system to distinguish between an isolated data-quality warning and an incident with a wider downstream blast radius.

The project deliberately does not claim a specific monetary industry cost for data-quality incidents because no such statistic is established in the supplied official hackathon materials or the current project evidence.

## Why Existing Solutions Fall Short

| Existing approach                 | Limitation                                                                                                                                             |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Basic data validation**         | Can identify that a rule failed on a dataset, but generally does not investigate the wider incident.                                                   |
| **Schema monitoring**             | Can flag a schema change, but does not necessarily determine whether it caused a downstream anomaly.                                                   |
| **Anomaly detection**             | Identifies unusual behavior but often stops at detection rather than tracing the incident.                                                             |
| **Data observability dashboards** | Provide freshness, volume, schema, and quality signals, but interpretation and cross-system investigation may remain manual.                           |
| **Lineage tools**                 | Show how data flows between systems, but the engineer still has to use that graph to investigate a particular incident and determine its blast radius. |
| **Manual investigation**          | Requires engineers to correlate logs, lineage, schemas, and timestamps repeatedly for each incident.                                                   |
| **Generic AI chatbots**           | Can generate explanations, but may fabricate metrics or conclusions when they are not grounded in structured evidence.                                 |
