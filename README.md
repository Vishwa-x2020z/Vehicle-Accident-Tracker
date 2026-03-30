# 🚨 Intelligent Accident Detection and Location Tracking Information System

> An IoT-based automatic vehicle accident detection system that uses accelerometer and vibration sensors to detect crashes, retrieves GPS coordinates, and instantly alerts emergency services via GSM SMS — all in real time.

---

## 📌 Overview

Road accidents are a leading cause of preventable deaths due to delays in emergency response. This project addresses that gap by building a fully automatic accident detection and alert system. When a collision or rollover is detected, the system:

1. Identifies the accident using accelerometer and vibration sensors
2. Fetches the exact GPS coordinates of the incident
3. Sends an SMS with a Google Maps link to police, hospital, and registered contacts — within seconds

**University Project** | B.E. in Electronics & Communication Engineering  
**Institution:** BLDEA's V.P. Dr. P.G. Halakatti College of Engineering & Technology, Vijayapura  
**Year:** 2023–24 | **Guide:** Prof. Jayashree N.C.

---

## 🛠️ Hardware Components

| Component | Model | Role |
|---|---|---|
| Microcontroller | Arduino UNO R3 (ATmega328P) | Central processing unit |
| GSM Module | SIM800L | Send SMS + call alerts |
| GPS Module | NEO-6M | Real-time location tracking |
| Accelerometer | ADXL335 (3-axis) | Detect rollover / tilt |
| Vibration Sensor | SW-18010P | Detect collision impact |
| LCD Display | 16x2 | Local status display |
| Power Supply | 9V DC / USB | System power |

---

## ⚙️ System Architecture

```
Vehicle Sensors
       │
       ├── ADXL335 Accelerometer (A0, A1, A2) ──► Detects rollover (X/Y axis threshold > 320)
       ├── SW-18010P Vibration Sensor (A3)    ──► Detects impact/collision
       │
       ▼
Arduino UNO R3 (ATmega328P)
       │
       ├── GPS NEO-6M (D6/D7 SoftwareSerial) ──► Fetch latitude & longitude
       ├── GSM SIM800L (D10/D11 SoftwareSerial) ──► Send SMS + Call
       └── LCD 16x2 (A4/A5 I2C) ──► Display status
             │
             ▼
    SMS to Police / Hospital / Home
    "Accident Detected! Vibration detect
     http://maps.google.com/maps?q=loc:16.848565,75.717293"
```

---

## 📂 Project Structure

```
accident-detection-system/
├── src/
│   └── accident_detection.ino    # Main Arduino sketch
├── hardware/
│   ├── circuit_diagram.png       # Full wiring schematic
│   └── prototype_photos/         # Hardware build photos
├── docs/
│   └── project_report.pdf        # Full project report (VTU)
├── simulation/
│   └── proteus_simulation.pdsprj # Proteus simulation file
└── README.md
```

---

## 🔌 Pin Configuration

| Component | Arduino Pin |
|---|---|
| GPS TX | D7 (SoftwareSerial RX) |
| GPS RX | D6 (SoftwareSerial TX) |
| GSM TX | D11 (SoftwareSerial RX) |
| GSM RX | D10 (SoftwareSerial TX) |
| Accelerometer X | A0 |
| Accelerometer Y | A1 |
| Accelerometer Z | A2 |
| Vibration Sensor | A3 |
| LCD RS | A4 |
| LCD EN | A5 |

---

## 🚀 Getting Started

### Prerequisites
- Arduino IDE (v1.8+)
- Libraries required:
```
SoftwareSerial (built-in)
LiquidCrystal (built-in)
TinyGPS++ (install via Library Manager)
```

### Upload & Run
```bash
# 1. Open Arduino IDE
# 2. Install TinyGPS++ from Library Manager
# 3. Open src/accident_detection.ino
# 4. Select Board: Arduino UNO
# 5. Select correct COM port
# 6. Click Upload
```

### Configure Alert Numbers
In the sketch, update the phone numbers to receive SMS alerts:
```cpp
#define POLICE_NUMBER    "+91XXXXXXXXXX"
#define HOSPITAL_NUMBER  "+91XXXXXXXXXX"
#define HOME_NUMBER      "+91XXXXXXXXXX"
```

---

## ⚡ How It Works — 3 Phases

### Phase 1: Accident Detection
- The ADXL335 accelerometer continuously monitors vehicle tilt on X, Y, Z axes
- If angle on X or Y axis exceeds threshold of **320** (indicating rollover), accident is flagged
- Simultaneously, the SW-18010P vibration sensor monitors for strong impact events
- Either trigger activates the alert sequence

### Phase 2: Location Tracking
- On accident detection, Arduino queries the NEO-6M GPS module
- GPS returns real-time latitude and longitude coordinates
- A Google Maps URL is constructed: `http://maps.google.com/maps?q=loc:<lat>,<lng>`

### Phase 3: Sending Notification
- SIM800L GSM module sends an SMS to all registered numbers
- Message includes: alert text + live Google Maps location link
- A phone call is also placed to the primary contact number
- LCD displays current system status throughout

---

## 📊 Results

- ✅ **Alert time:** SMS sent within ~3 seconds of accident detection
- ✅ **GPS accuracy:** Location pinpointed to within ~5m (NEO-6M)
- ✅ **Tested scenarios:** Rollover simulation, strong vibration impact, power-on cold start
- ✅ **Live demo:** Successfully called and messaged registered numbers with Google Maps link

### Demo Screenshots

| Prototype | SMS Alert | Location Tracking |
|---|---|---|
| Hardware assembled on test track with toy car | "Accident Detected! Vibration detect" + Maps link | Google Maps showing exact college location |

---

## ⚠️ Known Limitations

- Requires active GSM network coverage to send alerts
- GPS cold start takes ~30 seconds to acquire satellite lock
- False positives possible on very rough roads (tunable via threshold values)

---

## 🔮 Future Scope

- Integrate **heartbeat sensor** to assess victim condition and severity
- Add **camera module** for real-time video evidence capture
- Upgrade to **4G LTE** module (SIM7670) for faster data transmission
- Implement **edge AI** for smarter false-positive filtering
- Add **cloud dashboard** for fleet monitoring and historical data analysis
- Integrate **fire detection sensor** for post-crash fire alerts

---

## 📚 References

1. S. Sarker et al., *"An Approach Towards Intelligent Accident Detection, Location Tracking and Notification System"* — IEEE ICTP 2019
2. A. Bhakat et al., *"Vehicle Accident Detection & Alert System using IoT and AI"* — IEEE ASIANCON 2021
3. A. Ali and M. Eid, *"An automated system for Accident Detection"* — IEEE I2MTC 2015
4. N. Kattukkaran et al., *"Intelligent accident detection and alert system for emergency medical assistance"* — IEEE ICCCI 2017

---

## 👤 Author

**Vishwanath S. Goroshi** (2BL20EC114)  
B.E. Electronics & Communication Engineering  
📧 vishwa.goroshi@gmail.com | 📍 Bangalore, India  
🔗 [GitHub](https://github.com/Vishwa-x2020z)
