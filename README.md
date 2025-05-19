## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Getting Started](#getting-started)
  - [1. Training the Model](#1-training-the-model)
  - [2. Setting up ESPcam with Arduino](#2-setting-up-espcam-with-arduino)
  - [3. Integrating Zephyr RTOS](#3-integrating-zephyr-rtos)
# Object detection project on ESPcam using the Zephyr RTOS, leveraging TensorFlow for model training and deployment

This project implements object detection on an ESPcam to classify eggs using a TensorFlow Lite model. The data for training was sourced from [RoboFlow](https://roboflow.com/) and trained with TensorFlow. The ESPcam was set up with the Arduino IDE for deployment, and the Zephyr RTOS was configured for further enhancements.

---

## Project Overview
This repository demonstrates:
1. Training an object detection model using TensorFlow and RoboFlow data.
2. Converting the model to TensorFlow Lite format for deployment on microcontrollers.
3. Setting up and deploying the model on ESPcam using Arduino.
4. Integrating Zephyr RTOS for advanced features like task scheduling and resource management.

---

## Features
- Egg object detection using a custom-trained TensorFlow Lite model.
- Real-time inference on ESPcam.
- Lightweight deployment with Zephyr RTOS.

---

## Getting Started
Follow these steps to reproduce the project:

### 1. Training the Model
1. **Data Preparation**:
   - Collect egg image data using [RoboFlow](https://roboflow.com/).
   - Annotate the data for object detection (bounding boxes around eggs).
   - Export the dataset in a TensorFlow-supported format.

2. **Training the Model**:
   - Open this [Colab notebook template](https://colab.research.google.com/drive/1M9F4ohgpPpvrXIE0vtuU9cfbFOHzXeUc).
   - Upload your RoboFlow dataset.
   - Modify the notebook to load your data and adjust hyperparameters as needed.
   - Train the model until it achieves satisfactory accuracy.
   - Export the trained model to **TensorFlow Lite (.tflite)** format for microcontroller deployment.

---

### 2. Setting up ESPcam with Arduino
2. **Install ESP32 Board Support**:
   - Open **Preferences** in Arduino IDE.
   - Add this URL in the "Additional Board Manager URLs" field:
     ```
     https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
     ```
   - Go to **Tools > Board > Boards Manager**, search for **ESP32**, and install it.

3. **Connect and Configure ESPcam**:
   - Connect the ESPcam to your PC using a USB-to-serial adapter.
   - Select **AI Thinker ESP32-CAM** under **Tools > Board**.
   - Set the appropriate **Port** under **Tools > Port**.

4. **Deploying the Model**:
   - Use the [TensorFlow Lite for Microcontrollers library](https://github.com/tensorflow/tflite-micro).
   - Write Arduino code to load and run the `.tflite` model.
   - Configure the ESPcam to perform inference on the live video stream.

---

### 3. Integrating Zephyr RTOS
1. **Setting up Zephyr**:
   - Install Zephyr RTOS following the [official documentation](https://docs.zephyrproject.org/latest/getting_started/index.html).
   - Configure the ESP32 target board in Zephyr.
     ```bash
     west init -m https://github.com/zephyrproject-rtos/zephyr.git
     west update
     ```
   - Build the project:
     ```bash
     west build -b esp32 -p auto
     ```

2. **Zephyr Enhancements**:
   - Use Zephyr for task scheduling to separate the camera feed, inference, and system diagnostics into individual threads.
   - Implement power management features to optimize ESPcam performance.

3. **Flashing the Code**:
   - Flash the Zephyr-based firmware to the ESPcam using:
     ```bash
     west flash
     ```

---

