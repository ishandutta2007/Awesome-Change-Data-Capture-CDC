# Awesome-Change-Data-Capture-CDC

# Awesome-Change-Data-Capture-CDC
**Top Change Data Capture CDC (Opensource) 🌟 Star if you like it! 🌟**

**Curated List of SaaS Products & Open-Source GitHub Projects**
*Focused on Log-Based Replication, Streaming Ingestion, Schema Evolution & Database-to-Lakehouse Pipelines*
**Last updated: October 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Change Data Capture (CDC)**. These tools enable organizations to stream row-level changes (inserts, updates, deletes) from operational databases into data warehouses, lakes, and downstream applications—from fully managed platforms with zero-impact agents and schema evolution to open-source engines that give teams complete control over their replication topology and infrastructure.

**Examples** include Debezium, Qlik Replicate, Fivetran HVR, Striim, Estuary Flow, Arcion (Databricks), StreamSets, Hevo Data, AWS DMS, and Snowflake Streams (the category leaders in commercial and open-source space).

**Open-source emphasis**: This section is expanded with every relevant project for self-hosted CDC, streaming pipelines, and open replication infrastructure. **Critical note**: The open-source CDC landscape is dominated by **Debezium** as the de facto standard for log-based capture, but **Flink CDC** has emerged as a powerful alternative that eliminates the Kafka broker requirement for database-to-lakehouse pipelines . No open-source project matches Qlik Replicate's enterprise database coverage (including mainframe) or Fivetran HVR's zero-impact agent architecture at scale.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Qlik Replicate](https://www.qlik.com/)**
  **Enterprise CDC and replication platform** with broad source support including SAP and mainframe systems. **Pricing**: Quote-only; no published pricing . **Free tier**: None. **Best for**: enterprises needing high-volume CDC from legacy systems into Qlik analytics or other targets—**trade-off**: complex setup and unclear error reporting noted by users .

- **[Fivetran HVR](https://www.fivetran.com/)**
  **Real-time CDC replication** with zero-impact agent architecture. HVR captures changes directly from database transaction logs, maintaining full transactional integrity with minimal load on source systems. **Features**: HVR Hub (central brain), source/target locations, channels for pipeline definitions, agents placed close to source databases to read logs locally and encrypt data before transmission . **Pricing**: Quote-only. **Free tier**: None. **Best for**: enterprises needing low-impact, high-volume replication from Oracle, SQL Server, PostgreSQL, and SAP HANA into cloud warehouses—**trade-off**: enterprise pricing and deployment complexity.

- **[Striim](https://www.striim.com/)**
  **Unified data integration and streaming platform** with real-time CDC. **Pricing**: **Usage-based**: events from $100/million, vCPU from $0.50/hour, data transfer $0.10/GB in/out. **License-based**: per-core pricing with no data limits . Minimum 1-year contract. **Free tier**: Trial available. **Best for**: teams wanting a unified streaming platform for CDC plus analytics—**trade-off**: event-based pricing can escalate with high-frequency updates.

- **[Estuary Flow](https://estuary.dev/)**
  **Streaming data pipeline platform** with CDC capabilities. **Pricing**: **$0.50/GB** for data volume (captured + delivered); **$100/month per connector instance** for first 6, **$50/month** thereafter; first 10 GB and 2 connectors free . **Free tier**: Yes, 10 GB/month and 2 connectors. **Best for**: teams wanting transparent, usage-based pricing for CDC pipelines—**trade-off**: data volume is billed on both capture and delivery, doubling effective cost per GB moved.

- **[Arcion (Databricks)](https://www.databricks.com/)**
  **Real-time enterprise data replication** acquired by Databricks in 2023 for **over $100 million** . **Features**: Zero-impact, agentless CDC pipelines; connectors for 20+ enterprise databases; low-latency replication with built-in HA and schema evolution . **Pricing**: Now integrated into Databricks; quote-only. **Free tier**: None. **Best for**: Databricks customers wanting native CDC ingestion into the lakehouse—**trade-off**: ecosystem lock-in; standalone Arcion no longer available.

- **[StreamSets](https://streamsets.com/)** (IBM)
  **Smart streaming data pipelines** with graphical interface. **Pricing**: Starting at **$1,000/month** . **Free tier**: None. **Best for**: teams wanting visual pipeline design for hybrid and multicloud CDC—**trade-off**: premium pricing for a visual-first approach.

- **[Hevo Data](https://hevodata.com/)**
  **No-code ETL/ELT with real-time CDC**. **Pricing**: Starting at **$239/month**; transparent pricing with free tier . **Free tier**: Yes, 14-day trial. **Best for**: teams wanting simple, no-code CDC setup with 150+ connectors—**trade-off**: fewer connectors than Fivetran; simpler transformation capabilities.

- **[AWS Database Migration Service (DMS)](https://aws.amazon.com/dms/)**
  **Managed database migration and CDC** within AWS. **Pricing**: Instance-based or Serverless (DCU-based); storage ($0.08–$0.10/GB-month) and cross-AZ/region transfer costs apply . **Free tier**: AWS Free Tier applies to some usage. **Best for**: AWS-centric organizations migrating to RDS, Aurora, or Redshift with ongoing CDC—**trade-off**: requires careful instance sizing; replication lag can creep if undersized.

- **[Snowflake Streams](https://www.snowflake.com/)**
  **Native CDC within Snowflake** using stream objects that track changes to tables. **Pricing**: Consumption-based (Snowflake credits). **Free tier**: Trial credits available. **Best for**: Snowflake customers wanting CDC for transformations within the warehouse—**not** a database-to-warehouse replication tool.

## Open-Source GitHub Projects

- **[Debezium](https://github.com/debezium/debezium)**
  **Open source distributed platform for change data capture** (Apache 2.0) — **the de facto standard for log-based CDC**, with **18 source connectors and 25 sink connectors** . **Features**: Captures row-level changes from MySQL, PostgreSQL, MongoDB, Oracle, SQL Server, Db2, Cassandra, and more; streams changes into Kafka topics; **Kafka Connect compatible**—runs in a Connect cluster with horizontal scaling, automatic task rebalancing, and durable offsets stored in Kafka; **Single Message Transforms** for filtering and routing; Schema Registry integration for Avro/JSON/Protobuf; snapshot + incremental switching with exactly-once semantics (overlap deduplication) . **Tech stack**: Java. **Deploy**: Kafka Connect cluster (self-hosted or managed like MSK Connect) . **Trade-off**: **Requires Kafka**—adds operational overhead and infrastructure cost. Snapshot of large tables can create binlog backlog. Filtering on row values requires custom SMTs (Groovy/JavaScript scripting engine must be installed, with security implications) . **Best for**: teams with existing Kafka infrastructure or multi-consumer fanout requirements—the most mature, widely deployed open-source CDC platform with a proven track record at enterprise scale.

- **[Apache Flink CDC](https://github.com/apache/flink-cdc)**
  **Streaming ELT with CDC directly into Flink** (Apache 2.0) — **the most significant CDC architectural advance of 2024–2026**, eliminating the Kafka broker for database-to-lakehouse pipelines . **Features**: **Flink reads the database binlog itself** (embeds Debezium for MySQL, PostgreSQL, Oracle, MongoDB, SQL Server, Db2, Vitess, and more); **declarative YAML pipelines**—capture, transform, and route in one job; **SQL-like filtering before events are written** (transforms support computed columns, built-in functions, UDFs); **exactly-once semantics** with checkpoint-based recovery; consistent initial snapshot with seamless switch to incremental . **Tech stack**: Java (Flink). **Deploy**: Self-hosted Flink cluster. **Trade-off**: **No Kafka broker means no multi-consumer fanout**—downstream consumers must read from the destination (e.g., Iceberg table) rather than a topic. Best for point-to-point database-to-lakehouse sync where minute-level latency is acceptable; **sub-second latency or multiple independent consumers still require Kafka** . **Best for**: teams building database-to-Iceberg/Paimon lakehouse pipelines without Kafka overhead, or teams wanting filtering and transformation in a single Flink job before storage costs are incurred.

- **[Apache Paimon CDC](https://github.com/apache/paimon)**
  **Streaming lakehouse platform with native CDC ingestion** (Apache 2.0) — **a specialized CDC integration for Paimon tables**, part of the broader Paimon lakehouse project. **Features**: Native CDC ingestion from MySQL, PostgreSQL, Kafka, and other sources into Paimon tables; supports streaming upserts and changelog producers; designed for real-time lakehouse architectures. **Tech stack**: Java (Flink). **Deploy**: Self-hosted (Flink + Paimon). **Trade-off**: **Paimon-specific**—it ingests into Paimon tables, not Iceberg or Hudi. Smaller community than Debezium or Flink CDC. **Best for**: teams using Apache Paimon as their lakehouse table format wanting native CDC ingestion.

### Additional Strong Open-Source Options

- **Kafka Connect JDBC Source** — Query-based CDC via polling `WHERE updated_at > last_checkpoint`. **Note**: **Does not capture deletes**; depends on monotonic timestamp columns; periodic source database load. **Production recommendation: avoid unless binlog access is impossible** . **Best for**: legacy systems that cannot enable transaction log access.
- **Debezium Server** — Standalone Debezium runtime without Kafka Connect. Supports sinks like Iceberg (community). **Note**: Row-level filtering still requires SMTs; no Kafka ecosystem. **Best for**: teams wanting Debezium's capture engine without Kafka Connect infrastructure.

**Frameworks for building custom systems**: Combine **Debezium** for multi-consumer fanout with Kafka, **Flink CDC** for direct database-to-lakehouse pipelines without Kafka overhead, and **Paimon CDC** for Paimon-specific ingestion—creating a CDC stack matched to each team's latency and architectural requirements. **None of these match Qlik Replicate's mainframe/SAP coverage or Fivetran HVR's zero-impact agent architecture**; those require commercial platforms.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, license (for open-source), and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- CDC platforms handling database changes and replication must comply with data protection regulations (GDPR, CCPA, etc.) and implement appropriate access controls for replicated data.
- **The "log-based" vs. "query-based" vs. "trigger-based" distinction is critical.** **Log-based CDC** (Debezium, Flink CDC, Qlik Replicate, HVR, AWS DMS) reads database transaction logs—it is the **production standard**: minimal source impact, captures deletes, preserves order . **Query-based CDC** (Kafka Connect JDBC Source) polls with `WHERE updated_at > last_checkpoint`—it **cannot capture deletes**, depends on monotonic time columns, and adds periodic load to source databases. **Production recommendation: avoid query-based CDC unless binlog access is impossible** . **Trigger-based CDC** creates triggers in the source database—**rare in production** due to performance impact and maintenance burden. **Choose log-based CDC for any production workload.**
- **Debezium is the most mature and widely deployed open-source CDC platform.** With 18 source and 25 sink connectors under Apache 2.0, it is the foundation of most open-source CDC stacks . **The trade-off**: it requires Kafka, which adds operational overhead and cost. **Flink CDC eliminates that requirement** for database-to-lakehouse pipelines by reading binlogs directly and writing to Iceberg/Paimon—but loses multi-consumer fanout and sub-second latency .
- **Flink CDC is the architectural innovation to watch.** Druva's production case study (October 2026) demonstrates why: they replaced Debezium + Kafka with Flink CDC writing directly to Iceberg, filtering out ~90% of noise (backup job progress updates) before it hit storage . **For teams building database-to-lakehouse pipelines where minute-level latency is acceptable and Kafka is not already in place, Flink CDC is the pragmatic choice.**
- **Arcion is no longer a standalone product.** Databricks acquired it for over $100 million in 2023 and integrated its CDC connectors into the lakehouse platform . **Do not evaluate Arcion as an independent option**—it is now a Databricks feature.
- **Pricing opacity varies.** Qlik Replicate and Fivetran HVR are quote-only . Striim publishes usage-based and license-based tiers . Estuary publishes transparent per-GB and per-connector pricing . Hevo publishes starting at $239/month . AWS DMS is instance/DCU-based with storage and transfer costs . StreamSets starts at $1,000/month . **Validate with direct vendor conversations against your actual change volume and latency requirements.**
- Self-hosted open-source solutions require proper infrastructure (Kafka Connect cluster or Flink cluster, source database log access, schema registry), security hardening, and ongoing maintenance. **CDC pipelines carry business-critical data changes**—ensure your deployment includes monitoring for replication lag, schema change handling, and exactly-once guarantees before relying on it for production analytics.

---

**Made for data engineers, platform teams, and organizations building transparent change data capture solutions.**
Let's make Change Data Capture more open, data-driven, and replication-reliable.
