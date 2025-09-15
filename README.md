# ADXL345 Accelerometer Interface with Arduino UNO

![ADXL345 Accelerometer with Arduino](https://circuitdigest.com/sites/default/files/projectimage_mic/Interfacing-ADXL345-Accelerometer-with-Arduino-UNO_0.jpg)

## 📖 Project Overview

This [ADXL345 Accelerometer with Arduino project](https://circuitdigest.com/microcontroller-projects/interface-adxl345-accelerometer-with-arduino-uno) demonstrates how to interface the ADXL345 3-axis accelerometer with Arduino UNO to measure acceleration and detect motion in X, Y, and Z axes. The ADXL345 is a small, thin, ultralow power, 3-axis accelerometer with high-resolution measurement capabilities, making it perfect for motion sensing applications.

**Source Tutorial:** [Circuit Digest - Interface ADXL345 Accelerometer with Arduino UNO](https://circuitdigest.com/microcontroller-projects/interface-adxl345-accelerometer-with-arduino-uno)

## ✨ Features

- **3-Axis Motion Detection**: Measures acceleration in X, Y, and Z directions
- **Digital Interface**: Uses I2C communication protocol for easy interfacing
- **High Precision**: Provides accurate acceleration readings in m/s²
- **Low Power Consumption**: Ideal for battery-powered applications
- **Real-time Monitoring**: Continuous acceleration data display on Serial Monitor
- **Compact Design**: Small form factor suitable for wearable projects

## 🎯 Applications

This accelerometer interface can be used for various applications:

- **Vehicle Accident Detection Systems**: Detect sudden deceleration or impact
- **Hand Gesture Controlled Robots**: Control robots using hand movements
- **Earthquake Detection Alarms**: Detect seismic vibrations
- **Gaming Controllers**: Motion-based game control (Ping Pong games)
- **Mobile Phone Features**: Screen rotation and orientation detection
- **Fitness Trackers**: Step counting and activity monitoring
- **Industrial Monitoring**: Vibration analysis in machinery

## 🛠️ Components Required

| Component | Quantity | Description |
|-----------|----------|-------------|
| Arduino UNO | 1 | Main microcontroller board |
| ADXL345 Accelerometer | 1 | 3-axis digital accelerometer sensor |
| Breadboard | 1 | For making connections |
| Male-Female Jumper Wires | 4 | For connections between Arduino and sensor |

## 📋 Pin Configuration

### ADXL345 to Arduino UNO Connections:

| ADXL345 Pin | Arduino UNO Pin | Description |
|-------------|-----------------|-------------|
| VCC | 5V | Power supply (3.3V-5V) |
| GND | GND | Ground connection |
| SDA | A4 | I2C Data line |
| SCL | A5 | I2C Clock line |

## 🔌 Circuit Diagram

```
Arduino UNO          ADXL345
-----------          -------
    5V    ---------> VCC
   GND    ---------> GND
    A4    ---------> SDA
    A5    ---------> SCL
```

## 📚 Required Libraries

Before uploading the code, install the following libraries through Arduino IDE Library Manager:

1. **Adafruit ADXL345** - Main library for ADXL345 sensor
2. **Adafruit Unified Sensor** - Unified sensor driver
3. **Wire** - I2C communication library (pre-installed)

### Installation Steps:
1. Open Arduino IDE
2. Go to `Sketch` → `Include Library` → `Manage Libraries`
3. Search for "Adafruit ADXL345" and install
4. Search for "Adafruit Unified Sensor" and install

## 💻 Arduino Code

```cpp
#include <Wire.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_ADXL345_U.h>

// Create an instance of the ADXL345 sensor
Adafruit_ADXL345_Unified accel = Adafruit_ADXL345_Unified();

void setup(void) {
    // Initialize serial communication
    Serial.begin(9600);
    
    // Check if sensor is connected properly
    if(!accel.begin()) {
        Serial.println("No valid sensor found");
        while(1); // Stop execution if sensor not found
    }
    
    Serial.println("ADXL345 Accelerometer Test");
    Serial.println("X\t\tY\t\tZ\t\tUnits");
    Serial.println("================================");
}

void loop(void) {
    // Create event structure to store sensor data
    sensors_event_t event;
    
    // Get acceleration event data
    accel.getEvent(&event);
    
    // Display acceleration values
    Serial.print("X: "); Serial.print(event.acceleration.x); Serial.print(" ");
    Serial.print("Y: "); Serial.print(event.acceleration.y); Serial.print(" ");
    Serial.print("Z: "); Serial.print(event.acceleration.z); Serial.print(" ");
    Serial.println("m/s^2");
    
    // Wait 500ms before next reading
    delay(500);
}
```

## 🚀 How to Use

1. **Hardware Setup**:
   - Connect the ADXL345 sensor to Arduino UNO as per the pin configuration
   - Ensure proper power supply connections (5V and GND)
   - Double-check I2C connections (SDA to A4, SCL to A5)

2. **Software Setup**:
   - Install required libraries in Arduino IDE
   - Copy and paste the provided code
   - Select correct board (Arduino UNO) and port
   - Upload the code to Arduino

3. **Testing**:
   - Open Serial Monitor (set baud rate to 9600)
   - You should see acceleration readings in X, Y, Z axes
   - Gently move the sensor to observe changing values
   - Normal gravity reading should be approximately 9.8 m/s² on one axis

## 📊 Understanding the Output

- **X-axis**: Left-right movement
- **Y-axis**: Forward-backward movement  
- **Z-axis**: Up-down movement (shows ~9.8 m/s² when stationary due to gravity)
- **Units**: All readings are in meters per second squared (m/s²)

### Sample Output:
```
ADXL345 Accelerometer Test
X		Y		Z		Units
================================
X: 0.12 Y: 0.24 Z: 9.76 m/s^2
X: 0.08 Y: 0.31 Z: 9.81 m/s^2
X: 0.15 Y: 0.19 Z: 9.78 m/s^2
```

## 🔧 Troubleshooting

| Problem | Possible Cause | Solution |
|---------|---------------|----------|
| "No valid sensor found" | Wiring issues | Check I2C connections (SDA/SCL) |
| No output on Serial Monitor | Wrong baud rate | Set Serial Monitor to 9600 baud |
| Erratic readings | Loose connections | Ensure secure wiring |
| Constant zero values | Power supply issue | Check VCC and GND connections |

## 📈 Advanced Features

### Sensor Specifications (ADXL345):
- **Measurement Range**: ±2g, ±4g, ±8g, ±16g (programmable)
- **Resolution**: Up to 13-bit resolution
- **Interface**: I2C and SPI digital interfaces
- **Power Consumption**: As low as 23 μA in measurement mode
- **Operating Voltage**: 2.0V to 3.6V (with 5V tolerant I/O)

### Comparison with Other Accelerometers:
| Feature | ADXL345 | ADXL335 | ADXL356 |
|---------|---------|---------|---------|
| Interface | Digital (I2C/SPI) | Analog | Analog |
| Range | ±16g | ±3g | ±10g to ±40g |
| Power | 140µA | 350µA | 150µA |
| Pricing | Low | Lowest | High |

## 🌟 Project Extensions

1. **Data Logging**: Store acceleration data to SD card
2. **Wireless Monitoring**: Send data via WiFi/Bluetooth
3. **Threshold Alerts**: Trigger alarms for specific acceleration values
4. **Motion Patterns**: Detect specific movement patterns
5. **IoT Integration**: Send data to cloud platforms

## 📝 License

This project is open-source and available under the MIT License.

## 🤝 Contributing

Feel free to fork this project and submit pull requests for improvements.

## 📞 Support

For technical support or questions, refer to the original tutorial: 
[Circuit Digest ADXL345 Tutorial](https://circuitdigest.com/microcontroller-projects/interface-adxl345-accelerometer-with-arduino-uno)
[Arduino Projects](https://circuitdigest.com/arduino-projects)
---

**Happy Making! 🚀**
For technical support or questions, refer to the original tutorial: 
[Circuit Digest ADXL345 Tutorial](https://circuitdigest.com/microcontroller-projects/interface-adxl345-accelerometer-with-arduino-uno)
[Arduino Projects](https://circuitdigest.com/arduino-projects)

---

**Happy Making! 🚀**
