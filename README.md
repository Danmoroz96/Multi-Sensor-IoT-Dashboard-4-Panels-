# Multi-Sensor-IoT-Dashboard-4-Panels-
In this lab I extended IoT system by adding a new sensor, publishing it via MQTT, visualizing it in Grafana, creating a 4-panel monitoring dashboard

This project demonstrates a multi-stage IoT architecture. It simulates environmental sensors on a Sensor Node, transmits raw data via TCP Sockets to an Edge Gateway, and finally broadcasts structured data via MQTT for visualization in Grafana.

Sensor Descriptions
The system simulates three distinct environmental data points to provide a comprehensive view of the monitored area:

Temperature Sensor: Measures ambient thermal conditions.

Range: 20.00°C to 35.00°C.

Behavior: High-precision decimal values simulating a standard HVAC environment.

Humidity Sensor: Monitors the moisture level in the air.

Range: 40.00% to 80.00%.

Behavior: Simulates indoor relative humidity.

Light Sensor (Lux): Measures the intensity of light hitting the sensor.

Range: 100.00 to 1000.00 lx.

Behavior: Represents conditions ranging from a dim room to a bright office.

MQTT Topic Hierarchy
To ensure data modularity and efficient subscriptions, each sensor is mapped to a unique topic:

Sensor,MQTT Topic
Temperature,savonia/iot/temperature
Humidity,savonia/iot/humidity
Light,savonia/iot/light

