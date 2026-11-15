# SOME/IP Vehicle Speed Service

## Overview

This project demonstrates service-oriented communication between two vehicle-related software components using SOME/IP (Scalable service-Oriented Middleware over IP).

The system consists of a Vehicle Speed Service acting as the service provider and an Instrument Cluster Client acting as the service consumer. The provider simulates vehicle speed data and makes it available to the consumer through a SOME/IP service.

The Instrument Cluster Client discovers the service using SOME/IP Service Discovery, requests the current vehicle speed through the `GetSpeed` method, and subscribes to the `SpeedChanged` event to receive automatic speed updates.

The implementation uses Python and the `someipy` library on Ubuntu Linux. Both applications communicate over UDP through the loopback interface (`127.0.0.1`). Wireshark and tcpdump are used to capture and analyse SOME/IP communication.

## Technologies Used

- Python
- Linux (Ubuntu)
- SOME/IP Protocol
- someipy Library
- UDP Communication
- SOME/IP Service Discovery
- Wireshark
- tcpdump

## System Components

| Component | Role | Purpose |
|-----------|------|---------|
| SOME/IP Daemon | Service Discovery | Helps consumers discover available services |
| Vehicle Speed Service | Provider | Provides current vehicle speed and sends updates |
| Instrument Cluster Client | Consumer | Requests speed data and receives event notifications |

## SOME/IP Configuration

| Parameter | Value |
|-----------|-------|
| Service ID | `0x1234` |
| Instance ID | `0x5678` |
| GetSpeed Method ID | `0x0001` |
| SpeedChanged Event ID | `0x8001` |
| Event Group ID | `0x0001` |
| Provider Endpoint | `127.0.0.1:3000` |
| Consumer Endpoint | `127.0.0.1:3002` |
| Service Discovery Port | `30490` |
| Multicast Address | `224.224.224.245` |
| Transport Protocol | UDP |

## Communication Features

- **Service Discovery:** Consumer discovers the Vehicle Speed Service through the SOME/IP daemon.
- **GetSpeed Method:** Implements request-response communication to retrieve the current vehicle speed.
- **SpeedChanged Event:** Sends automatic speed updates to subscribed consumers.
- **Event Group Subscription:** Allows the consumer to receive speed notifications whenever the value changes.

## Project Files

| File | Purpose |
|------|---------|
| `vehicle_speed_interface.py` | Defines service IDs, method IDs, event IDs, event groups, and payload format |
| `vehicle_speed_service.py` | Implements the Vehicle Speed Service provider |
| `cluster_client.py` | Implements service discovery, method calls, and event subscriptions |
| `someipyd.json` | Contains SOME/IP daemon configuration |

## Execution

1. Start the SOME/IP daemon.
2. Run `vehicle_speed_service.py` to start the provider.
3. Run `cluster_client.py` to start the consumer.
4. Verify service discovery and GetSpeed responses.
5. Check SpeedChanged event notifications.
6. Capture network traffic using Wireshark on the loopback interface (`lo`).

## Wireshark Analysis

- Captured SOME/IP Service Discovery traffic.
- Analysed UDP communication between provider and consumer.
- Observed GetSpeed request and response packets.
- Identified Service ID `0x1234` and Method ID `0x0001`.
- Analysed SpeedChanged event notifications.
- Used **Decode As** to identify UDP application traffic as SOME/IP in Wireshark.

## Key Observations

| Communication | Direction | Purpose |
|---------------|-----------|---------|
| Service Discovery | Consumer / Provider ↔ Multicast | Service availability discovery |
| GetSpeed Request | Consumer → Provider | Requests current vehicle speed |
| GetSpeed Response | Provider → Consumer | Returns current vehicle speed |
| SpeedChanged Notification | Provider → Consumer | Sends updated speed values |

## Learning Outcomes

- Understanding SOME/IP service-oriented communication.
- Implementing service provider and consumer applications.
- Understanding Service Discovery.
- Working with method-based and event-based communication.
- Understanding SOME/IP service, method, event, and event-group identifiers.
- Capturing and analysing network packets using Wireshark and tcpdump.
