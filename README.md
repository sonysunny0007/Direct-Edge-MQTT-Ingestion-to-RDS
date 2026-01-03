# Direct-Edge-MQTT-Ingestion-to-RDS

Architecture Overview
Edge Device → MQTT → AWS IoT Core → Processing → Amazon RDS (PostgreSQL)
Edge devices publish JSON telemetry using MQTT
AWS IoT Core acts as the managed MQTT broker
Incoming messages are processed and validated
Telemetry data is stored in Amazon RDS for querying and analytics

Tech Stack
Protocol: MQTT
Cloud Platform: AWS
IoT Broker: AWS IoT Core
Database: Amazon RDS (PostgreSQL)
Compute (planned): AWS Lambda
OS (development): macOS
