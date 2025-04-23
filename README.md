# ESPHome_ESP-C6
Example project that shows how to flash your ESP32-C6 board with ESPHome using the Arduino framework. To get this to work, some libraries that are natively in ESPHome are ignored and replaced by their up-to-date namesakes. These libraries are added via their respective git repositories. Next, a local, slightly modified version of ESPHome was created where *web_server_base.h* and *captive_portal.h* were modified. Instead of override, these header files simply define some functions, as these were not present in the imported libraries yet.

To get this work it is required that you have installed [Python](https://www.python.org/downloads/) and [git](https://git-scm.com/downloads). Next, follow these steps:

- Navigate to the folder where you want to clone the project.
- In this folder, open a terminal.
- Type `git clone git@github.com:IMMRMKW/ESPHome_ESP32-C6.git`
- Still using the terminal, navigate to the folder containing the cloned project.
- In this folder, create a virtual environment by using `python -m venv .venv`.
- Start the virtual environment using `.\.venv\Scripts\activate`
- Install ESPHome using `pip install ./esphome`
- Connect the ESP32-C6 to your laptop/computer using a USB cable.
- Note down the number of the COM port that is assigned to the ESP32-C6.
- In the *ESPHome_ESP32-C6* folder, create a file called *secrets.yml*. Copy-paste the contents of *secrets_example.yml* to the new file. Replace the wifi_ssid and wifi_password strings with the credentials that apply for your wifi. You can generate a Home Assistant Api key [here](https://esphome.io/components/api.html) (the site randomly generates a key upon accessing or refreshing the site). The access point credentials you can decide upon yourself.
- In your terminal, type `esphome run config.yml --device COM<number>`. Replace <number> with the number that is assigned to the COM port of your ESP32-C6. Press Enter. **Note**: if this is the first time you are uploading ESPHome to your ESP32-C6, PlatformIO will start downloading the platform packages. By default, the board file for *esp32-c6-devkitc-1* does not accept uploading code using the Arduino framework. The compiler will give the following error: `Error: This board doesn't support arduino framework!`. You will have to do the following:
    - Navigate to `%USERPROFILE%\.platformio\platforms\espressif32\boards`
    - Open *esp32-c6-devkitc-1.json* in a text editor.
    - Add `"arduino"` to the `"frameworks"` section, and `"variant": "ESP32C6"` to the `"build"` section. Your new json file looks as follows:
    ```
    {
  "build": {
    "core": "esp32",
    "f_cpu": "160000000L",
    "f_flash": "80000000L",
    "flash_mode": "qio",
    "mcu": "esp32c6",
	"variant": "ESP32C6"
  },
  "connectivity": [
    "wifi"
  ],
  "frameworks": [
    "espidf",
	"arduino"
  ],
  "name": "Espressif ESP32-C6-DevKitC-1",
  "upload": {
    "flash_size": "8MB",
    "maximum_ram_size": 327680,
    "maximum_size": 8388608,
    "require_upload_port": true,
    "speed": 460800
  },
  "url": "https://docs.espressif.com/projects/espressif-esp-dev-kits/en/latest/esp32c6/esp32-c6-devkitc-1/index.html",
  "vendor": "Espressif"
}
    ```
The configuration should now be compiled an be uploaded to your ESP32-C6.
