This project is designed to stream real-time temperature and humidity data using a Dockerized MQTT (Mosquitto) broker and Python’s Paho MQTT client, seamlessly integrating with ThingsBoard and Firebase Realtime Database for automated storage and visualization. Leveraging containerized microservices to orchestrate sensor-to-cloud data pipelines, the system ensures robust and modular data ingestion and processing. The alarm rule chain in ThingsBoard detects threshold-exceeding data, sending critical alerts to Firebase for immediate oversight. By uniting Docker, MQTT, and cloud-based platforms, this project demonstrates a full-stack IoT solution, showcasing the potential for proactive data-driven insights and real-time analytics.

### Tools:
* Python
* JSON
* ThingsBoard
* Firebase
* Libraries: Paho.mqtt
