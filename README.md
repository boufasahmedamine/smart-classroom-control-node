# Smart Classroom Control Node

An ESP32-based IoT edge node for classroom access control, attendance tracking, and classroom automation through a distributed MQTT architecture.

## Overview

The Smart Classroom Control Node is an embedded system developed as part of a Master's project in Automation and Industrial Computing at Frères Mentouri Constantine 1 University. It is designed to modernize conventional classrooms by combining secure RFID-based access control, automated attendance tracking, occupancy-aware automation, and centralized monitoring.

Each classroom is equipped with an ESP32 controller that interfaces with local sensors and actuators while communicating with a central server over MQTT. The node is responsible for hardware control and event reporting, whereas authorization, attendance management, and long-term data storage are handled by the server. This separation keeps the firmware lightweight, modular, and easier to maintain while allowing multiple classroom nodes to be managed from a single backend.

## Features

- RFID-based classroom access control using dual RDM6300 readers
- RFID attendance tracking with server-side logging
- Occupancy detection using the HLK-LD2410 mmWave radar sensor
- Automatic lighting control based on classroom occupancy
- Projector control through relay outputs
- MQTT communication with a centralized server
- Distributed edge-node architecture with server-side authorization
- Layered firmware architecture for modularity and maintainability
- FreeRTOS-based task scheduling for responsive operation
- Manual override controls for door access and lighting

- ## System Architecture

The Smart Classroom Control Node follows a distributed architecture in which each classroom is equipped with an independent ESP32-based control node. The node is responsible for interacting with local hardware, while a central server manages authorization, attendance records, and system supervision.

```text
                 MQTT over Wi-Fi
+------------------------+        +------------------------------+
|     Central Server     |<------>|  Smart Classroom Control Node|
|------------------------|        |------------------------------|
| • User Authorization   |        | • ESP32-WROOM-32            |
| • Attendance Database  |        | • RFID Readers              |
| • Event Logging        |        | • LD2410 Occupancy Sensor   |
| • Classroom Management |        | • Relay Outputs             |
+------------------------+        | • Local Automation          |
                                  +--------------+---------------+
                                                 |
                       +-------------------------+------------------------+
                       |             |                |                  |
                 Door Lock       Lighting        Projector        Status LEDs
```

The ESP32 acts as a lightweight edge controller. It reads sensors, controls actuators, publishes events through MQTT, and executes classroom automation logic. Decisions requiring centralized data—such as user authorization and attendance management—are handled by the server.
