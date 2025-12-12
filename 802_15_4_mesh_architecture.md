# Mesh arquitecture using 802.15.4

## 1. Introduction and Objectives

This laboratory exercise introduces the fundamentals of the IEEE 802.15.4 Physical (PHY) and Medium Access Control (MAC) layers. It lays the groundwork for developing IoT networks through practical frame analysis and channel management on ESP32-C6 devices.

### 1.2 Objectives
* Understand the 2.4 GHz channelization and 802.15.4 frame structure.
* Capture and classify different frame types: Beacon, Data, Acknowledgment (Ack), and MAC Command.
* Evaluate the impact of CCA (Clear Channel Assessment) threshold and CSMA-CA backoff parameters on communication performance.

## 2. Project setup guide
This section details the steps taken to set up and configure the lab environment using the ESP-IDF CLI in a Linux workstation.

### 2.1 Environment setup
Make sure to follow the installations steps of the [Standard Toolchain Setup for Linux and macOS](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/get-started/linux-macos-setup.html) and in the step 3 install the tools for the `esp32c6`

```bash
cd ~/esp/esp-idf
./install.sh esp32,esp32s2
```

Then export the environment variables that include the `idf.py` command. for that type:

```
. ./export.sh
```

If you're using a fish shell or any other option modify the commands. After that you should see an output like this:

<img width="1512" height="412" alt="image" src="https://github.com/user-attachments/assets/a9c62e67-c93d-4d6e-a3d1-dfe720a78f4a" />

### 2.2 Example selection and build command

For this example, we'll build the IEEE 802.15.4 CLI example:

```
cd examples/ieee802154/ieee802154_cli
idf.py set-target esp32c6
idf.py build
```

### 2.3 Flash the board

Make sure to connect via USB your ESP32C6 COM port and that you can see it as a `/dev/ttyACM` file:
idf
<img width="1513" height="63" alt="image" src="https://github.com/user-attachments/assets/c91073b8-9ca2-4706-9db2-10f146bcd2c5" />

```
idf.py flash -p /dev/ttyACM0
```

### 2.4 Monitor

To interact with the CLI and send commands use:

```
idf.py monitor -p /dev/ttyACM0
```

You should see a terminal similar to this:

<img width="733" height="121" alt="image" src="https://github.com/user-attachments/assets/b237da68-8938-4cab-ae3f-be7f8df775c9" />

## 3. Configurations

You can test the following parameters and play with their values.

|Parameter|Command|Example Value Set|Read Command|
|---|---|---|---|
|Channel|channel -s <ch>|channel -s 15|channel -g|
|Tx Power|txpower -s <dBm>|txpower -s 10|txpower -g|
|PAN ID|panid <id>|panid 0x1234|panid -g|
|Short Address|shortaddr <addr>|shortaddr 0x0001|shortaddr -g|
|Extended Address|extaddr <byte0> ... <byte7>|extaddr 0xaa 0xbb ... 0x33|extaddr -g|

<img width="865" height="525" alt="Screenshot 2025-12-02 211941" src="https://github.com/user-attachments/assets/05ca63b4-4308-44e3-9376-14446cd64a3a" />

To configure the coordinator and the node set the following values in two ESP32C6:

|Parameter|Device A (Coordinator)|Device B (Node)|
|---|----|---|
|PAN ID|panid 0x1234|panid 0x1234|
|Short Address|shortaddr 0x0001|shortaddr 0x0002|
|Channel|channel -s 15|channel -s 15|
|Operating Mode|rx -r 1 (Receiver mode)|N/A (Transmitter mode for data)|

Then you can send information via the `tx` command:

<img width="1900" height="666" alt="Screenshot 2025-12-02 212203" src="https://github.com/user-attachments/assets/aab06fd8-08d4-4aca-b9dd-dc4fd7c984b2" />


## 4.
