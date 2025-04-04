# Precision Landing

```diff
- This feature is only meant to be used for testing and development purposes.
- I will not be responsible for any damage or injury.
- Please do not try this example if you are not well versed with ArduPilot
```

![Demo](../docs/images/prec_land.gif)

## Running example on IOT devices

1. Plug in the camera using the supplied USB-C cable to your computer (Also attach the power cable to your wall outlet)

2. Inside the project directory (while the camera is connected) run:
```bash
python3 main.py
```
3. A OpenCV window should pop up with the Cameras IR view on it.

4. Print the landing target which can be found [here](../docs/images/precland_marker.png). Point the landing target towards the camera.

5. The camera should detect the target as well as print its 3-D coordinates.

6. If the above script works well, you can flash the pipeline to the camera so that a companion computer isn't required anymore.
Update the bootloader (only required once):
``` bash
python3 pipeline_uploader.py bootloader
```
Then upload the pipeline by running the command:
``` bash
python3 pipeline_uploader.py
```

6. Wait for a few seconds. Once the flash is complete, you should hear a "click" sound and the camera will automatically run the script every time it is powered up.

## Setting up ESP32

1. Connect the ESP32 via USB-B cable to your computer.

2. Setup the IDF environment via the guide [here](https://docs.espressif.com/projects/esp-idf/en/v4.2.2/esp32/get-started/index.html). If you are on Linux you might need to run (make sure you do this in a separate terminal as this opens up a virtual env):
```bash
. $HOME/esp/esp-idf/export.sh
```
3. Upload the script to ESP32. Make sure you enter the right port for the ESP32.
```bash
idf.py -p /dev/ttyUSB0  flash monitor
```
4. You should see the coordinates being printed on the screen If its printed, your setup is working!

## Setting up ArduPilot

1. Connect the Serial Pins and Ground to any serial port on your Flight Controller as shown below.
![Connections](../docs/images/connections.png)

2. Setup the following parameters:
- SERIALX_PROTOCOL = 2 (MAVLink)
- SERIAL4_BAUD = 115

3. Set up Precision Landing:
- PLND_ENABLED = 1
- PLD_TYPE = 1 (MAVLink)
- PLND_ALT_MAX = 7

4. Reboot

5. Open Mission Planner. Connect to the Flight Controller. Press Cntl + F to view the advanced menu. Click on "MAVLink Inspector"

6. If everything is set up well: A 1HZ Heartbeat should be visible there from a source ID "93".

7. Inflight switch to Land mode.

