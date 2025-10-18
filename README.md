# Smart-Irrigation
An IoT project dashboard aimed at water conservation. This front-end application simulates a smart irrigation system, allowing users to visualize sensor data on a live chart and manage watering schedules. Built with HTML, CSS, and JavaScript with localStorage for persistence.
# 💧 Smart Irrigation System (Java & Arduino)

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status](https://img.shields.io/badge/status-completed-brightgreen)

A hardware-based Smart Irrigation System that uses an Arduino microcontroller to automate plant watering. This project features a Java Swing desktop application that connects to the Arduino via a USB cable for real-time sensor monitoring and data logging to a MySQL database.

---

### 📸 Project Showcase
**java GUI Screenshot:**

<img width="998" height="597" alt="Screenshot 2025-10-18 122311" src="https://github.com/user-attachments/assets/5efa8e61-1906-49e2-996d-437832a4edbc" />
<img width="1920" height="1200" alt="Screenshot 2025-10-18 122233" src="https://github.com/user-attachments/assets/604006d6-c681-4e48-8890-4904734c6304" />
(This is the perfect place to add a photo of your assembled hardware circuit and a screenshot of your Java Swing application running!)

---

### ✨ Key Features

* *🤖 Automated Watering:* The Arduino automatically activates a water pump via a relay module when the soil moisture level drops below a predefined threshold.
* *🖥 Real-time Desktop Dashboard:* A multi-threaded Java Swing application provides a live GUI to display up-to-the-second data from all connected sensors.
* *🌡 Multi-Sensor Monitoring:* Utilizes a capacitive soil moisture sensor for accurate soil readings and a DHT11 sensor for ambient air temperature and humidity.
* *📈 Sensor Data Logging:* All incoming sensor data is timestamped and saved to a MySQL database, creating a historical log for analysis.
* *🔌 USB Serial Communication:* A reliable connection between the Arduino hardware and the Java software is established using serial communication over a USB cable.

---

### 🛠 Technology Stack

#### Hardware
* *Microcontroller:* Arduino Uno R3
* *Sensors:* Capacitive Soil Moisture Sensor, DHT11 Temperature & Humidity Sensor
* *Actuator:* 5V Single-Channel Relay Module
* *Pump:* Mini Submersible Water Pump (DC 3V-6V)

#### Software
* *Languages:* Java (JDK 11+), C++ (for Arduino)
* *Desktop GUI:* Java Swing
* *Database:* MySQL (or SQLite)
* *Connectivity:*
    * *JDBC:* For connecting the Java application to the database.
    * *JSerialComm Library* (or similar): For handling serial communication between Java and the Arduino.
* *IDE:*
    * Arduino IDE
    * IntelliJ IDEA or Eclipse for the Java application.

---

### ⚙ System Architecture

The system operates in a continuous loop. The sensors, physically placed in the plant's environment, send analog and digital signals to the Arduino. The Arduino code processes these signals, checks them against the watering threshold, and sends a command to the relay to control the pump.

Simultaneously, the Arduino packages the sensor readings into a formatted string (e.g., "Moisture:550,Temp:28,Hum:65") and sends it over the USB serial port every few seconds. The Java Swing application on the PC listens to this port, parses the string, updates the GUI with the new values, and executes an SQL INSERT statement to log the data into the database.

+------------------+
               |       User       |
               +--------+---------+
                        |
            (Views Data on the Application)
                        |
                        v
          +-----------------------------+
          |      Java Swing GUI         |
          |      (On a PC/Laptop)       |
          +-------------+---------------+
                        |
      +-----------------+-----------------+
      |                                   |
(Stores & Reads Log Data)           (Live Data via USB)
      |                                   |
      v                                   v
+--------------+            +-----------------------------+
|   Database   |            |    Arduino Microcontroller  |
| (MySQL/SQLite)|            +-------------+---------------+
+--------------+                          |
                        +-----------------+-----------------+
                        |                                   |
           (Reads Sensor Values)             (Sends ON/OFF Signal)
                        |                                   |
                        v                                   v
             +---------------------+             +---------------------+
             |       Sensors       |             |      Actuators      |
             | (Soil Moisture, DHT11)|             | (Relay -> Water Pump) |
             +---------------------+             +---------------------+


---

### 🚀 How to Set Up and Run

1.  *Hardware Setup:*
    * Assemble the circuit according to the provided circuit diagram (circuit-diagram.png).
    * Connect the sensors and relay to the correct pins on the Arduino.

2.  *Arduino Setup:*
    * Open the .ino sketch file in the Arduino IDE.
    * Select your board (Arduino Uno) and the correct COM Port from the "Tools" menu.
    * Click "Upload" to flash the code onto the microcontroller.

3.  *Database Setup:*
    * Ensure you have a MySQL server running.
    * Create a new database (e.g., smart_irrigation_db).
    * Execute the provided database_schema.sql script to create the SensorLog table.

4.  *Java Application Setup:*
    * Open the Java project in your IDE (IntelliJ or Eclipse).
    * Add the JSerialComm and MySQL JDBC Connector JAR files to your project's build path/dependencies.
    * In the Java code, update the database connection string (URL, username, password) and the serial port name (e.g., "COM3") to match your system.

5.  *Run the System:*
    * Connect the Arduino to your PC with the USB cable.
    * Run the Main.java (or equivalent) file from your IDE.
    * The Java Swing GUI should appear and start displaying live data from the sensors.

---

### 🔮 Future Scope

* *Web Dashboard:* Migrate the local Java Swing GUI to a web-based dashboard using HTML/CSS/JS for remote access from any device.
* *Wireless Connectivity:* Replace the USB connection with a Wi-Fi module (like the ESP8266) to make the hardware truly wireless and IoT-enabled.
* *API Development:* Create a backend server with a REST API to handle data, allowing multiple clients (web, mobile app) to connect and control the system.

---
             
