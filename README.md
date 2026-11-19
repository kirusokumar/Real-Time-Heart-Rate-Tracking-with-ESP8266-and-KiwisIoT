# Real-Time Heart Rate Tracking with ESP8266 and KiwisIoT

An IoT-based heart-rate monitoring prototype using NodeMCU ESP8266 and a pulse sensor to estimate heart rate in beats per minute (BPM) and visualize the readings on the KiwisIoT cloud dashboard.

## Project Overview

In this project, I built an IoT-based heart-rate tracking prototype using a NodeMCU ESP8266, pulse sensor, and KiwisIoT.

The sensor detects changes in its optical signal when a fingertip is placed on it. The ESP8266 reads the signal, estimates heart rate using the time interval between detected pulses, and sends the calculated BPM value to KiwisIoT through Wi-Fi.

The dashboard displays the received readings in a chart, making it easier to observe changes over time.

**System Data Flow:**

Fingertip → Pulse Sensor → NodeMCU ESP8266 → BPM Calculation → Wi-Fi → KiwisIoT → Dashboard

## Features

- Pulse sensor signal monitoring
- Heart-rate estimation in BPM
- Threshold-based pulse detection
- Serial Monitor output
- Wireless data transmission using ESP8266
- Real-time dashboard visualization
- Remote monitoring through KiwisIoT

## Hardware Components

| Component | Quantity |
|---|---:|
| NodeMCU ESP8266 | 1 |
| ProtoCentral Pulse Oximeter & Heart Rate Sensor based on MAX30100 | 1 |
| Jumper Wires | As required |
| USB-A to Mini-USB Cable | 1 |

## Software Requirements

- Arduino IDE
- ESP8266 Board Package
- KiwisIoT Arduino Library
- KiwisIoT Account
- Wi-Fi Connection

## Circuit Connections

The project instructions describe an analog pulse sensor connection.

| Pulse Sensor Pin | NodeMCU ESP8266 |
|---|---|
| VCC | 3.3V, if supported by the sensor |
| GND | GND |
| Signal / OUT | A0 |

**Important hardware clarification:** The Hackster component list identifies the sensor as a MAX30100-based module, but the wiring and Arduino code describe an analog-output pulse sensor connected to A0. A MAX30100 normally communicates over I2C and does not provide the analog output expected by this code. Verify your exact sensor model before wiring or uploading the sketch. The supplied code is for an analog pulse sensor.

Also verify that the sensor output does not exceed the permitted A0 input voltage of your particular ESP8266 board.

## KiwisIoT Dashboard Configuration

The calculated BPM value is transmitted to KiwisIoT through Channel 1.

| Channel | Parameter | Unit |
|---|---|---|
| Channel 1 | Estimated Heart Rate | BPM |

Create a chart or numeric display widget in your KiwisIoT dashboard and configure it to receive Channel 1 data.

## Arduino Programming

The program reads the analog pulse signal from A0 and uses threshold-based logic to detect possible heartbeats.

It calculates BPM using the time interval between consecutive detected pulses.

### BPM Calculation

\[
BPM = \frac{60,000}{\text{Beat interval in milliseconds}}
\]

For example, an interval of 800 milliseconds corresponds mathematically to 75 BPM.

Replace the Wi-Fi credentials and KiwisIoT Topic ID with your own values before uploading the code.

## Understanding the Code

- `HEART_PIN` defines the analog input used for the pulse sensor.
- `threshold` determines when a possible heartbeat is detected.
- `beatDetected` prevents repeated detections while the signal remains above the threshold.
- `millis()` measures the time interval between detected pulses.
- `60000UL / beatInterval` calculates the estimated BPM.
- `kiwisiot.send("1", bpm)` transmits the calculated BPM to Channel 1.

The threshold value of 550 is a starting value, not a universal setting. It may need adjustment depending on the sensor and signal quality.

## How It Works

1. Place a fingertip gently on the pulse sensor.
2. The sensor produces an analog signal that changes with variations in the detected optical signal.
3. The NodeMCU ESP8266 reads the signal through A0.
4. The program detects possible pulses using a threshold.
5. It calculates the time interval between consecutive detections.
6. The calculated BPM is printed in the Serial Monitor.
7. The ESP8266 sends accepted BPM readings to KiwisIoT through Channel 1.
8. The dashboard displays the received values in a chart or numeric widget.

## Installation and Setup

1. Install the Arduino IDE.
2. Install the ESP8266 board package through Boards Manager.
3. Select NodeMCU 1.0 (ESP-12E Module), or the matching option for your board.
4. Install the KiwisIoT Arduino library.
5. Connect the compatible analog pulse sensor to the NodeMCU.
6. Create a KiwisIoT dashboard and copy its Topic ID.
7. Enter your Wi-Fi credentials and Topic ID in the Arduino sketch.
8. Select the correct COM port.
9. Upload the program.
10. Open the Serial Monitor at 115200 baud.
11. Check Channel 1 on your KiwisIoT dashboard.

## Testing the Pulse Sensor

- Place your fingertip gently on the sensor's sensing area.
- Keep your finger still and avoid pressing too hard.
- Wait for the sensor signal to stabilize.
- Observe the calculated BPM in the Serial Monitor.
- Adjust the threshold if the signal is not detected reliably.
- Compare the dashboard values with the Serial Monitor output.

Movement, poor finger placement, ambient light, and signal noise can affect the readings.

## Applications

- Educational pulse-sensor experiments
- IoT-based physiological signal demonstrations
- Remote sensor-data visualization
- Embedded systems learning
- Wireless monitoring prototypes
- Biomedical electronics learning projects

## Troubleshooting

**No BPM values appear**
- Check sensor power and wiring.
- Verify the analog signal connection to A0.
- Check whether the threshold is suitable for the sensor.
- Keep your finger still while testing.

**BPM readings fluctuate**
- Check finger placement.
- Reduce movement during measurement.
- Inspect the raw analog signal for noise.
- Adjust the threshold according to the observed signal.

**KiwisIoT dashboard does not display data**
- Verify Wi-Fi credentials.
- Check the KiwisIoT Topic ID.
- Confirm that Channel 1 is configured correctly.
- Check the Serial Monitor for calculated BPM values.

**Sensor does not work with A0**
- Verify whether your sensor actually provides an analog output.
- A MAX30100 module uses I2C and requires a different wiring arrangement and compatible program.

## Safety Disclaimer

This project is an educational electronics prototype, not a medical device. The simple threshold-based algorithm is not clinically validated and may produce inaccurate readings. Do not use this project for diagnosis, treatment, emergency monitoring, or medical decisions.

## Libraries and Resources

- **KiwisIoT Website:** https://www.kiwisiot.in/
- **KiwisIoT Arduino Library:** https://github.com/Kiwistron/KiwisIoT
- **KiwisIoT Example Projects:** https://github.com/Kiwistron/KiwisIoT-Projects/tree/main

## Project Tutorial

Read the complete project tutorial on Hackster.io:

[Real-Time Heart Rate Tracking with ESP8266 and KiwisIoT](https://www.hackster.io/kirusokumar/real-time-heart-rate-tracking-with-esp8266-and-kiwisiot-3da4bc)

## Author

**Kirusokumar**

## License

This project is intended for educational and experimental purposes. You may modify and improve it with appropriate credit to the original author.