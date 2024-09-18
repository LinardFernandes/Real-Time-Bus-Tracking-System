# Real Time Bus Tracking System

This Arduino project integrates an ESP32/ESP8266 microcontroller with RFID and GPS modules to track bus entries and exits. It uses Firebase Realtime Database to log and manage bus passenger data. The project includes functionalities for:
- Connecting to Wi-Fi
- Communicating with Firebase Realtime Database
- Reading RFID tags
- Capturing GPS data
- Updating passenger count and balance based on RFID interactions

## Table of Contents

1. [Components Required](#components-required)
2. [Libraries](#libraries)
3. [Connections](#connections)
4. [Configuration](#configuration)
5. [Code Explanation](#code-explanation)
6. [Troubleshooting](#troubleshooting)
7. [License](#license)
   
## Components Required

- **ESP32** or **ESP8266** microcontroller
- **MFRC522** RFID reader
- **GPS module** (e.g., NEO-6M)
- **LEDs** (Green and Yellow)
- Breadboard and jumper wires

## Libraries

Ensure you have the following libraries installed in your Arduino IDE:
- `Firebase_ESP_Client` for Firebase integration
- `TinyGPS++` for GPS data handling
- `MFRC522` for RFID reader interaction
- `SoftwareSerial` for GPS serial communication (for older versions of Arduino IDE)

You can install these libraries through the Arduino Library Manager or by downloading them from GitHub.

## Connections

**RFID Reader Connections:**
- **SDA** -> D2 (GPIO 4)
- **RST** -> D1 (GPIO 5)

**GPS Module Connections:**
- **RX** -> D3
- **TX** -> D4

**LED Connections:**
- **Green LED** -> GPIO 15
- **Yellow LED** -> GPIO 16

Make sure to connect the GND and VCC pins of the RFID reader and GPS module to the GND and 3.3V (or 5V, depending on the module) of the ESP32/ESP8266, respectively.

## Configuration

### 1. Wi-Fi Credentials

Replace the placeholders with your Wi-Fi credentials:

```cpp
#define WIFI_SSID "your_wifi_ssid"
#define WIFI_PASSWORD "your_wifi_password"
```

### 2. Firebase Setup

Replace the placeholders with your Firebase project details:

- API Key: Obtain from your Firebase project settings.

```cpp
#define API_KEY "your_firebase_api_key"
```
- Database URL: Obtain from your Firebase Realtime Database settings.

```cpp
#define DATABASE_URL "your_firebase_database_url"
```

### 3. Firebase Paths and RFID UIDs

Update the Firebase paths and RFID UIDs according to your project needs:

- Database Paths: The database paths used in the code are:

```cpp
#define BUS_DATA_PATH "BusDet/8qpT8V1i0L40F5aFeyqy/"
#define UID_PATH "kvFldVC3vIchgIVKlvoDUpA9byr2"
#define BALANCE_PATH "Balance"
```

- RFID UIDs: The RFID UIDs used in the code:
 
```cpp
String uid1 = "01 94 E1 26";
String uid2 = "30 15 B5 20";
String uid3 = "60 27 5B 21";
```

Adjust these UIDs and paths according to the tags and database structure you are using.

## Code Explanation

- **Setup Function:**
  - Connects to Wi-Fi.
  - Initializes RFID and GPS modules.
  - Configures Firebase with API key and database URL.
  - Signs up for Firebase access and prints connection status.

- **Loop Function:**
  - Continuously reads GPS data and processes RFID interactions.
  - Updates Firebase database with bus entry and exit information.
  - Manages LED indicators based on RFID interactions and bus capacity.

- **RFID Processing (`rfids` Function):**
  - Checks for new RFID card presence.
  - Reads card UID and updates Firebase with entry/exit status.
  - Updates GPS data, bus count, and passenger balance in Firebase.
  - Manages LED indicators based on the bus capacity.

## Troubleshooting

- **Wi-Fi Connection Issues:**
  - Ensure the ESP32/ESP8266 is within range of the Wi-Fi network.
  - Check Wi-Fi credentials for correctness.

- **Firebase Errors:**
  - Verify API Key and Database URL are correctly inserted.
  - Ensure Firebase project has necessary permissions and is correctly configured.

- **RFID and GPS Issues:**
  - Check wiring and connections.
  - Ensure RFID tags are properly read by the MFRC522 reader.
  - Verify that the GPS module is receiving signals (check the serial monitor for GPS data).

## License

This project is open-source and free to use. Feel free to modify and distribute it as needed.
