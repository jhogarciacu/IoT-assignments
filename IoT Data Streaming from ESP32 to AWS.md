# Cloud-Connected ESP32 Using MQTT over WiFi

### 1. Introduction an objetives
This project demonstrates how to connect an ESP32 device to a cloud server using WiFi and MQTT.
The objective is to establish a reliable IoT communication pipeline where the ESP32 publishes sensor data to an AWS-hosted MQTT broker and receives cloud-issued commands to change the color of an onboard or external RGB LED.

### 2. Requirements 
-  ESP32-C6
-  WiFi network
-  MQTT broker running on AWS (EC2, AWS IoT Core, or custom server)
-  MQTT client library for ESP32 (ESP-IDF or Arduino PubSubClient)

### 3. Project setup guide
This section provides a quick and professional guide to set up the project, including firmware configuration, MQTT server preparation, and LED control testing.

### 3.1 Hardware Preparation
-  ESP32-C6 development board
-  RGB LED or built-in addressable LED (depending on the board)
-  USB cable
-  Stable WiFi connection

### 3.2 MQTT Broker Installation (Mosquitto on Windows)
  1. Download Mosquitto from the official site:
    [Instalar Mosquitto](https://mosquitto.org/download)
  2. Install Mosquitto and ensure the option “Install service” is enabled.
  3. Navigate to the Mosquitto installation folder, typically:
```
C:\Program Files\Mosquitto\

```
### 3.3 Mosquitto Configuration File
Create or edit a configuration file called mosquitto.conf:
```
listener 1883
allow_anonymous true

```
Save this file in the Mosquitto folder.

### 3.4 Start the MQTT Broker
Run Mosquitto with the custom configuration:
```
mosquitto -v -c mosquitto.conf

```
<img width="1275" height="148" alt="image" src="https://github.com/user-attachments/assets/e8b9f056-5cb1-4ee1-8823-fdb390483321" />

If everything is correct, you should see logs like:
```
Opening ipv4 listen socket on port 1883

```
### 4. WiFi Configuration Requirements
nside your firmware, ensure you configure:
```
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
const char* mqtt_server = "YOUR_PC_LOCAL_IP";  // Example: 192.168.0.12

```
### Important:
-  The PC running Mosquitto
-  And the ESP32
Must be connected to the same WiFi network, or the ESP32 will NOT reach the broker

### 4.1 To obtain your PC’s IP address:
```
ipconfig

```
<img width="927" height="831" alt="image" src="https://github.com/user-attachments/assets/19f165c3-728b-4535-a60b-6e2e23f8523f" />

Use the IPv4 Address (e.g., 192.168.1.11).

### 5. Firmware Build & Deployment
  1. Navigate to the Firmware Directory
```
cd "YOUR FOLDER PATH"

```
  2. Build the Firmware
```
idf.py build

```
<img width="1600" height="755" alt="image" src="https://github.com/user-attachments/assets/20d5c010-981f-491a-82c1-f91a3bb4a851" />

  3. Flash the Firmware to the ESP32
```
idf.py -p "YOUR PORT (COM)" flash

```
<img width="1600" height="757" alt="image" src="https://github.com/user-attachments/assets/431726f8-4c21-43e2-9549-975a723c8a90" />

  4. Open the Serial Monitor
```
idf.py -p "YOUR PORT (COM)" monitor

```
<img width="1428" height="600" alt="image" src="https://github.com/user-attachments/assets/5532cd75-7d90-47c2-bb7a-40383fffd37c" />

# Visualitation proyect
<img width="949" height="330" alt="image" src="https://github.com/user-attachments/assets/aeb30113-8e38-4d65-9553-4a276c00ab1f" />


  


