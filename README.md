# MicroSpotter: Embedded Object Detection System with Arduino
Creators: Andrew Esch, Lauren Roe, Zach Pederson

## Hardware Requirements
The MicroSpotter system uses two Arduino devices, one Arduino to recognize speech input and the other to detect objects. Any Arduino that supports TinyML, a microphone module, and camera module could operate with this repository. However, these models are optimized for Arduino Nano 33 BLE sense. Thus, the following hardware is required:
- 2 Arduino Nano 33 BLE Sense Devices
- 2 Arduino Tiny Machine Learning Shields
- 2 USB A to Micro USB Cables
- 1 OV7675 Camera Module (for the object detection model)
- 1 Computer running Windows 8+ (tested), macOS (untested), or Linux (untested)

To purchase these two Arduinos as a complete bundle, see the official [Arduino Tiny Machine Learning Kit](https://store-usa.arduino.cc/products/arduino-tiny-machine-learning-kit) at Arduino's official store.

Note: Please ensure that the primary computer running MicroSpotter meets the minimum hardware specifications to run Arduino IDE and Python concurrently.


## Software Requirements
To run MicroSpotter, please install the following software:
- [Arduino IDE](https://www.arduino.cc/en/software)
- [Python 3.x](https://www.python.org/)
- [Jupyter Notebook](https://jupyter.org/install)
- Optional: An IDE that supports Python (e.g., [VSCode](https://code.visualstudio.com/))


## Arduino IDE Library Requirements
In addition to installing Arduino IDE, please install the "OV767X" library. This library is required to operate the camera for the object detection model. You can also find it available in Arduino IDE at the following link.
- http://librarymanager/All#Arduino_OV767X

### Python 3.x Package Requirements
In addition to installing Python 3.x, MicroSpotter requires the following Python packages:
- serial
- google-cloud-textto-speech
- playsound
- pyttsx3


To install this with one command on a CLI, copy and paste this into your terminal. Make sure pip is calling the associated Python installation that MicroSpotter will be working with.
```
pip install serial --upgrade google-cloud-texttospeech playsound pyttsx3
```


## Model Installation Guide
This repository comes included with two Edge Impulse models that are optimized for TinyML with TensorFlow Lite on Arduino Nano 33 BLE Sense, and are packaged here as zip files. These zip files are custom libraries that can be installed directly in Arduino IDE:
- ei-handheld-detection-arduino-1.0.16.zip: Object Detection Model
- ei-handheld-voice-recognition-arduino-1.0.4.zip: Speech Recognition Model


To install these zip folders, open Arduino IDE and navigate to *Sketch > Include Library > Install .ZIP Libary...* and upload both of the folders individually. These libraries should become available under *File > Examples* as the following:
- handheld-detection-inferencing: Object Detection Model
- handheld-voice-recognition-inferencing: Speech Recognition Model

If these libraries do not become visible immediately upon uploading, please restart Arduino IDE. Otherwise, please reference [Arduino's documentation site](https://docs.arduino.cc/software/ide-v1/tutorials/installing-libraries#importing-a-zip-library) for debugging details.

Next, attach all of the required hardware modules to both of the Arduino Nano 33 BLE Sense devices (see hardware list above and instructions from the Arduino Tiny ML learning kit) and connect them to the primary computer device via USB. These two Arduinos should appear as separate devices under the Boards list in Arduino IDE. **IMPORTANT: Please Note the COM numbers for each connected Arduino device, and decide which model you will use for each COM device. You will need this for later when running MicroSpotter with Python.** 

Then, open the following examples in Arduino IDE in two new windows:
- *File > Examples > handheld-detection-inferencing > nano_ble33_sense > nano_ble33_sense_camera*: Object Detection Model Example
- *File > Examples > handheld-voice-recognition-inferencing > nano_ble33_sense > nano_ble33_sense_microphone*: Speech Recognition Model Example

Once each example is open in a new window, deploy each of the models to each of the two devices separately by pressing "Compile". The deployment process will take approximately 10-15 minutes for each model.


## Running MicroSpotter
Once each model is deployed, verify that each model is running within Arduino IDE by viewing each device within the serial monitor. If both models appear to show some type of output, then it is safe to proceed with running MicroSpotter.

To run MicroSpotter, start by completely closing out of Arduino IDE and opening the "handheld-detection.ipynb" file. Then, modify the "COM" parameters in these lines to match your device setup.
- voice_controller = serial.Serial(**'COM4'**, 9600)
- object_controller = serial.Serial(**'COM5'**, 9600)

Finally, run all cells within the handheld-detection file to run MicroSpotter!

To exit MicroSpotter, either press "CTRL-C" or terminate the cell through Jupyter Notebook.


## Using MicroSpotter
Once MicroSpotter is running, set up some objects nearby the camera (see supported item list below). Then, speak close to the microphone on the speech recognition Arduino and say one of the following phrases to use MicroSpotter:
- "What is this": Detects and lists out all of the objects currently visible to the camera.
- "How many objects": Counts and states the number of detected objects currently visible to the camera.


### Supported Items List for MicroSpotter
- Eraser
- Mouse
- Pencil
- Remote
- VR Controller
- Water Bottle


## Explanation Videos
- [Model Creation Video](https://www.loom.com/share/44e2444ede474335b93aaa3fdbaaa121)
- [Demo Video](https://www.loom.com/share/c1bbb918fa3e4f7da630826beb280d75)


## Additional Documentation
See the following [Google doc](https://docs.google.com/document/d/1gCw1OeW_1MnZxHt1P3Tb5WjdUbuWuRKVG33-ymkoPgQ/edit) to view a full breakdown about how MicroSpotter was developed and implemented.
