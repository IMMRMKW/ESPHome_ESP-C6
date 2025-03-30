# ESPHome_ESP32-C6
Example project that shows how to flash your ESP32-C6 board with ESPHome using the Arduino framework. To get this work it is required that you have installed [Python](https://www.python.org/downloads/) and [git](https://git-scm.com/downloads). Next, follow these steps:

- Navigate to the folder where you want to clone the project.
- In this folder, open a terminal.
- Type `git clone git@github.com:IMMRMKW/ventimate.git`
- Still using the terminal, navigate to the folder containing the cloned project.
- In this folder, create a virtual environment by using `python -m venv`.
- Start the virtual environment using `.\.venv\Scripts\activate`
- Install ESPHome using `pip install esphome`
- Connect the ESP32-C6 to your laptop/computer using a USB cable.
- Note down the number of the COM port that is assigned to the HA Mate.
- In the *ESPHome_ESP32-C6* folder, create a file called *secrets.yml*. Copy-paste the contents of *secrets_example.yml* to the new file. Replace the wifi_ssid and wifi_password strings with the credentials that apply for your wifi. You can generate a Home Assistant Api key [here](https://esphome.io/components/api.html) (the site randomly generates a key upon accessing or refreshing the site). The access point credentials you can decide upon yourself.
- In your terminal, type `esphome run config_ESP32_S3.yml --device COM<number>`. Replace <number> with the number that is assigned to the COM port of your HA Mate. Press Enter.

The configuration should now be compiled and uploaded to your ESP32-C6.
