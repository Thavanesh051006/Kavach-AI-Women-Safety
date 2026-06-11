# 🛡️ Kavach AI: Proactive Women & Child Safety System

## 1. Project Title
**Kavach AI: A Proactive IoT & Full-Stack Enabled Women and Child Safety System**

## 2. Problem Statement
Existing personal safety applications are predominantly **"Reactive"** in nature. They rely heavily on manual user intervention, requiring a distressed individual to physically unlock their smartphone and trigger an SOS button. In critical real-world scenarios—such as extreme panic, physical restraint, sudden assaults, or forced immobilization via sedatives (e.g., Chloroform)—the victim is rendered incapable of accessing their device. Therefore, there is a critical need for an automated, **"Proactive"** safety ecosystem that detects threats using bio-signals and automated behavioral analysis without requiring any human action.

## 3. Project Objectives
* **Proactive Threat Detection:** Automatically identify distress or a state of unconsciousness by analyzing parameters like heart-rate drops and absolute immobility.
* **Standalone Execution:** Ensure uninterrupted protection using independent IoT wearables, eliminating dependency on smartphones during critical crises.
* **Infrastructure-Independent Tracking:** Transmit emergency data through specialized long-range radio networks (**LoRa Mesh Network**), bypassing traditional cellular network dead-zones.
* **Tamper-Proof Evidence Management:** Securely stream real-time audio/video recordings directly to a remote cloud server the moment a threat is detected.

## 4. Module List
1. **IoT Wearable Sensor Module:** Manages continuous data acquisition using integrated physiological sensors (`MAX30102` for heart-rate/SpO2 and `MPU6050` for sudden fall/posture tracking).
2. **Frontend Dashboard Module:** A responsive web panel built using `React` and styled with `Bootstrap` for guardians and police control rooms to track real-time locations dynamically on an interactive map.
3. **Backend Central Server Module:** Powered by `Java + Spring Boot`, this core layer processes incoming REST API streams from devices, executes threat-validation logic, and communicates with the database layer.
4. **Automated Notification & Emergency Module:** Handles immediate dispatch routines, triggering real-time automated alerts and live GPS routing links to emergency handlers via dedicated `SMS/Email APIs`.

## 5. Technical Stack Architecture
| Architectural Layer | Technologies Implemented | Functional Scope / Implementation Purpose |
| :--- | :--- | :--- |
| **Frontend UI/UX** | HTML5, CSS3, Bootstrap, React | Renders the single-page real-time tracking interface and police control dashboard. |
| **Backend API Gateway** | Java + Spring Boot | Handles business logic, processes multi-sensor payloads, and hosts microservices. |
| **Database Layer** | MongoDB | Serves as a high-throughput NoSQL storage solution ideal for handling rapidly updating real-time GPS coordinate streams. |
| **Security & Middleware** | JWT Authentication, REST APIs, SMS Notification | Enforces secure encrypted authentication tokens for data privacy and dispatches transactional emergency alerts. |

## 6. Database Schema Design (Collection / Table List)

### Table 1: `Users` (User & Child Profile Registry)
| Field Name | Data Type | Key Constraints | Description |
| :--- | :--- | :--- | :--- |
| `user_id` | ObjectId / String | Primary Key | Unique system identifier for the registered user. |
| `name` | String | None | Full legal name of the female user or child. |
| `age` | Integer | None | Age parameter used for baseline biometric tuning. |
| `guardian_phone` | String | None | Primary emergency contact number for instant SMS alerts. |
| `device_id` | String | Unique Key | Unique hardware MAC Address of the paired IoT band. |

### Table 2: `Live_Tracking` (Real-Time Sensor Streams)
| Field Name | Data Type | Key Constraints | Description |
| :--- | :--- | :--- | :--- |
| `track_id` | ObjectId / String | Primary Key | Unique transaction log ID. |
| `device_id` | String | Foreign Key | Relates the tracking telemetry to a specific IoT device. |
| `latitude` | Double | None | Current real-time global GPS Latitude coordinate. |
| `longitude` | Double | None | Current real-time global GPS Longitude coordinate. |
| `heart_rate` | Integer | None | Continuous beats-per-minute (BPM) telemetry input. |
| `status` | String | None | System state categorization: `Normal` / `High Alert` / `Unconscious`. |
| `timestamp` | DateTime | None | Exact system millisecond epoch time of the packet delivery. |

### Table 3: `Emergency_Alerts` (Incident Management Console)
| Field Name | Data Type | Key Constraints | Description |
| :--- | :--- | :--- | :--- |
| `alert_id` | ObjectId / String | Primary Key | Unique ticket ID generated per emergency dispatch event. |
| `user_id` | String | Foreign Key | References the exact victim involved in the incident. |
| `last_location` | String | None | String-concatenated geo-coordinates recorded at trigger time. |
| `alert_type` | String | None | Classification of threat origin: `Panic Audio` / `Biological Drop` / `Fall`. |
| `police_status` | String | None | Live response management status tracking: `Dispatched` / `Resolved`. |
