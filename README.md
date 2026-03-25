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

Sensor - Temperature, MQTT Topic - savonia/iot/temperature

Sensor - Humidity, MQTT Topic - savonia/iot/humidity

Sensor - Light, MQTT Topic - savonia/iot/light

Dashboard Layout & Explanation
The Grafana dashboard is designed for high-glanceability, using a 4-panel layout to separate historical trends from real-time status.

![Screenshot 2026-03-25 141501](https://github.com/user-attachments/assets/890afb5e-a100-4583-90e3-b93d00316547)
![Screenshot 2026-03-25 141521](https://github.com/user-attachments/assets/76475b1e-f07b-438f-ac6f-e7fc70282ba8)
![Screenshot 2026-03-25 141650](https://github.com/user-attachments/assets/f311d5ef-113a-4a6d-a9c6-38e3494c095c)
![Screenshot 2026-03-25 143356](https://github.com/user-attachments/assets/26675650-5a8d-4d33-b78e-1403ed132f12)
![Screenshot 2026-03-25 144711](https://github.com/user-attachments/assets/f3bc83d2-54b1-4230-8f49-f56a30805fe6)
![Screenshot 2026-03-25 143553](https://github.com/user-attachments/assets/6ab460ba-6a80-4265-a34e-ff9f84ebddf7)
![Screenshot 2026-03-25 143613](https://github.com/user-attachments/assets/03d99333-0990-4087-bd6b-0550d065303e)
![Screenshot 2026-03-25 144604](https://github.com/user-attachments/assets/9760b53e-8e6b-46c8-ad55-6f4fe9c97135)
![Screenshot 2026-03-25 144625](https://github.com/user-attachments/assets/7f68476c-2922-4d7c-aa5c-a07b50f9ce8b)
![Screenshot 2026-03-25 144711](https://github.com/user-attachments/assets/335b111b-2302-49d8-964b-78d6f91094d0)
![Screenshot 2026-03-25 145105](https://github.com/user-attachments/assets/10ba4610-7287-48e6-a99c-a61e7e2ab086)
![Screenshot 2026-03-25 145121](https://github.com/user-attachments/assets/c1481704-5dfe-40b2-a036-9ea0d2e76cda)
![Screenshot 2026-03-25 145146](https://github.com/user-attachments/assets/a0c0d01a-d310-4273-a123-a5df669c3844)
![Screenshot 2026-03-25 145201](https://github.com/user-attachments/assets/c9399824-9fd2-470a-9abc-b2b649068fa2)

Layout Breakdown
Panel 1: Temperature Graph (Time Series)

Occupies the top half of the dashboard. This allows the user to see fluctuations and trends over time rather than just a single data point.

Panel 2: Humidity Gauge

A circular gauge showing the current moisture percentage. Includes color thresholds (e.g., green for 40-60%) to indicate "comfort zones."

Panel 3: Light Gauge

Displays the current Lux value. Scaled from 0 to 1000 to provide a visual representation of brightness levels in the room.

Panel 4: Status Panels

Located at the bottom, these panels show the "Current State" in large text. They are configured to change color if sensors exceed specific safety thresholds (e.g., turning Red if the temperature exceeds 30°C).

How to Test

Run the Edge Device on Laptop 2 (or same laptop but in different window): python edge_device.py

Run the Sensor Node on Laptop 1: python socket_sensor.py

Ensure the SERVER_IP in socket_sensor.py matches the local IP of Laptop 2.


Why do we separate each sensor into a different MQTT topic?

Granular Subscriptions (Efficiency)
MQTT is built on a Publish/Subscribe model. If a specific device (like a smart thermostat) only needs to know the temperature to function, it can subscribe only to savonia/iot/temperature  (for example).

Efficiency: The device doesn't waste battery, CPU cycles, or bandwidth parsing a large string containing humidity and light data that it doesn't intend to use.

Using unique topics allows you to use wildcards (+ and #) to organize data logically.

Differing Data Rates

Not all sensors "age" at the same rate.

Temperature changes slowly; you might only need to publish it every 60 seconds.

Motion or Light might need to be near-instant (sub-second).

By separating them, each sensor can have its own sampling frequency, preventing the slow data from being bogged down by the fast data.

Simplified Metadata
The Topic Name effectively acts as the metadata for the value. When the subscriber receives a message on savonia/iot/light, it already knows the unit is Lux and the context is "Light" before it even looks at the numeric value. 

This removes the need for complex "packet headers" or CSV parsing logic on the receiving end.










