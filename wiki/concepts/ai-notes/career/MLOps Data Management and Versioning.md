---
type: concept
title: "MLOps Data Management and Versioning"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mlops
  - mlops
complexity: beginner
domain: mlops
status: developing
address: c-000307
related:
  - "[[AI-Notes Study Roadmap]]"
  - "[[Python Serialization]]"
sources:
  - "[[.raw/repos/AI-Notes/MLOPS/Data Management.md]]"
---

# MLOps: Data Management and Versioning

[[ai-notes|AI-Notes]]' MLOps folder has 13 pages, but only two contain text (`Data Management.md`, `Version Control.md`). The rest (Automation, CI/CD, DVC, Docker, Experiment Tracking, Git, Governance, Kubeflow Pipelines, MLflow, Monitoring and Retraining, Provisioning) are empty placeholders: a planned syllabus.

## Data management

Which parts matter depends on the system (annotation is central at Tesla, for example, but irrelevant for many NLP pipelines).

| Stage | What | Tools |
|-------|------|-------|
| **Ingestion** (Extract) | Pull from databases, real-time streams, APIs | Python, **Kafka** |
| **Transformation** (Transform) | Clean and reshape | Python, **PySpark / Spark** |
| **Storage** (Load) | **Warehouse** (structured) vs **lake** (unstructured; S3 as object store) | MySQL, Oracle, MongoDB, Snowflake, BigQuery, S3 |
| ETL orchestration | | AWS Glue, Informatica, Apache NiFi |

## Versioning everything (not just code)

| What | Tool |
|------|------|
| Code | **Git** (GitHub) |
| Data and models | **DVC** |
| Experiments and model registry | **MLflow** |
| Environments | **Docker** |
| Pipelines | **Kubeflow Pipelines** |

Git alone isn't enough for ML: reproducibility needs the exact data, model artifacts, environment and pipeline versions too. Model artifacts are stored by serialization ([[Python Serialization]]).

> [!gap] Most MLOps pages are empty in the source
> Experiment tracking, CI/CD, monitoring and retraining are listed but unwritten.
