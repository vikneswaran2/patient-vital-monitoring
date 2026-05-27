# Patient Vital Monitoring Streaming Pipeline

## Overview
<img width="1536" height="1024" alt="ChatGPT Image May 27, 2026, 08_30_03 PM" src="https://github.com/user-attachments/assets/26051ca7-4f72-4643-8cd1-6742361d3c39" />
<img width="1307" height="737" alt="image" src="https://github.com/user-attachments/assets/33026eb0-0b05-425c-b08d-7d4408b11e04" />

This project is a real-time healthcare streaming analytics pipeline built using modern cloud-native data engineering technologies on Google Cloud Platform.

The system simulates live patient health vitals including:

- Heart Rate
- Oxygen Saturation (SpO2)
- Body Temperature
- Blood Pressure

Streaming patient data is ingested through Google Cloud Pub/Sub, processed in real time using Apache Beam and Google Cloud Dataflow, organized using a Medallion Architecture (Bronze, Silver, Gold), and finally stored in BigQuery for analytics and dashboarding.

---

## Key Features

- Real-time streaming ingestion
- Apache Beam streaming ETL pipeline
- Google Cloud Dataflow processing
- Pub/Sub event streaming
- Bronze, Silver, and Gold medallion architecture
- Data validation and error filtering
- Risk score calculation
- Streaming aggregation
- BigQuery analytics integration
- Cloud-native data engineering workflow

---

## Medallion Architecture

### Bronze Layer

Stores raw patient streaming data exactly as received from Pub/Sub.

Purpose:
- Raw historical archive
- Data replay capability
- Auditing
- Debugging
- Immutable source of truth

### Silver Layer

Stores cleaned and validated records after:
- JSON parsing
- Null filtering
- Invalid record rejection
- Risk score enrichment

Purpose:
- Analytics-ready data
- Machine learning preparation
- Clean healthcare streams

### Gold Layer

Stores aggregated healthcare analytics including:
- Average Heart Rate
- Average SpO2
- Average Temperature
- Maximum Risk Level

Purpose:
- Dashboarding
- Monitoring systems
- Business analytics
- Healthcare insights

---

## Risk Scoring Engine

The pipeline computes a real-time patient risk score using:
- Heart Rate
- Body Temperature
- Oxygen Saturation (SpO2)

### Risk Levels

| Risk Score | Risk Level |
|------------|------------|
| < 0.3 | Low |
| 0.3 - 0.6 | Moderate |
| > 0.6 | High |

---

## Streaming Workflow

### Step 1 — Data Simulation

A Python simulator continuously generates synthetic patient vitals.

### Step 2 — Pub/Sub Streaming

Messages are streamed into Google Cloud Pub/Sub.

### Step 3 — Dataflow Processing

The Apache Beam pipeline:
- Reads streaming data
- Validates records
- Filters invalid events
- Enriches records with risk scores
- Aggregates metrics

### Step 4 — Bronze and Silver Storage

Data is stored in Google Cloud Storage.

### Step 5 — Gold Analytics

Aggregated metrics are written into BigQuery.

### Step 6 — Visualization

BigQuery can connect to:
- Looker Studio
- Tableau
- Power BI

---

## Error Injection System

The simulator intentionally generates corrupted records for realistic testing.

### Injected Errors

- Missing fields
- Negative heart rate values
- Invalid SpO2 values

This helps test:
- Data validation
- Fault tolerance
- Streaming robustness

---

## Example Streaming Record

```json
{
  "patient_id": "P001",
  "heart_rate": 110.5,
  "spo2": 92.3,
  "temperature": 38.4,
  "bp_systolic": 130.2,
  "bp_diastolic": 82.1,
  "risk_score": 0.67,
  "risk_level": "High"
}
```

---

## BigQuery Analytics

The Gold Layer stores:
- Patient-level summaries
- Aggregated streaming analytics
- Risk monitoring insights

### Example Use Cases

- ICU monitoring
- Critical patient alerts
- Hospital dashboards
- Historical trend analysis

---

## Technologies Used

| Technology | Purpose |
|------------|---------|
| Python | Pipeline Development |
| Apache Beam | Streaming ETL |
| Google Cloud Dataflow | Distributed Processing |
| Google Cloud Pub/Sub | Event Streaming |
| Google Cloud Storage | Bronze and Silver Layers |
| BigQuery | Gold Analytics Layer |
| python-dotenv | Environment Management |

---

## Setup Instructions

### Install Dependencies

```bash
pip install 'apache-beam[gcp]' python-dotenv google-cloud-pubsub
```

### Environment Variables

Create a `.env` file:

```env
GCP_PROJECT=your-project-id

PUBSUB_SUBSCRIPTION=your-subscription

BRONZE_PATH=gs://your-bucket/bronze/
SILVER_PATH=gs://your-bucket/silver/

BIGQUERY_TABLE=project.dataset.table

TEMP_LOCATION=gs://your-bucket/temp/
STAGING_LOCATION=gs://your-bucket/staging/

REGION=us-central1
```

---

## Run Simulator

```bash
python patient_vitals_simulator.py
```

---

## Run Dataflow Pipeline

```bash
python streaming_medallion_pipeline.py \
  --runner DataflowRunner \
  --project $GCP_PROJECT \
  --region $REGION \
  --staging_location $STAGING_LOCATION \
  --temp_location $TEMP_LOCATION \
  --streaming
```

---

## Learning Outcomes

This project demonstrates:
- Real-time streaming architecture
- Apache Beam programming
- Google Cloud Dataflow
- Pub/Sub integration
- Medallion architecture
- Cloud-native ETL
- Streaming aggregation
- BigQuery warehousing
- Distributed processing

---

## Future Improvements

- Real-time alert system
- Looker Studio dashboard
- Vertex AI risk prediction
- Stateful stream processing
- Time-series anomaly detection
- Parquet optimization
- BigQuery partitioning
- ML-based risk classification

---

## Author

Viknesh  
Data Engineering and Streaming Analytics Project
