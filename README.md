# ESPHome_ESP-C6
Example project that shows how to flash your ESP32-C6 board with ESPHome using the Arduino framework. To make this work, some libraries that are natively in ESPHome are ignored and replaced by their up-to-date namesakes, which are added via their respective git repositories. Next, a local, slightly modified version of ESPHome was created. *web_server_base.h* and *captive_portal.h*, instead of override, these header files simply define some functions, as these were not present in the imported libraries yet.

To get this work it is required that you have installed [Python](https://www.python.org/downloads/) and [git](https://git-scm.com/downloads). Next, follow these steps:

- Navigate to the folder where you want to clone the project.
- In this folder, open a terminal.
- Type `git clone git@github.com:IMMRMKW/ESPHome_ESP32-C6.git`
- Still using the terminal, navigate to the folder containing the cloned project.
- In this folder, create a virtual environment by using
    - `python -m venv .venv` on Windows.
    - `source ./venv/bin/activate` on Linux.
- Start the virtual environment using `.\.venv\Scripts\activate`
- Install ESPHome using `pip install ./esphome`
- Connect the ESP32-C6 to your laptop/computer using a USB cable.
- Note down the port number that is assigned to the ESP32-C6.
    - On Windows, you can identify the port number using Device Manager.  
    - On Linux, you can use the `dmesg | grep tty` command to identify the port.
- In the *ESPHome_ESP32-C6* folder, create a file called *secrets.yaml*. Copy-paste the contents of *secrets_example.yaml* to the new file. Replace the wifi_ssid and wifi_password strings with the credentials that apply for your wifi. You can generate a Home Assistant Api key [here](https://esphome.io/components/api.html) (the site randomly generates a key upon accessing or refreshing the site). The access point credentials you can decide upon yourself.
- In your terminal, type 
    - `esphome run config.yaml --device COM<number>` on Windows.
    - `esphome run config.yml --device /dev/ttyACM<number>` on Linux.

    Replace `<number>` with the number that is assigned to the COM port of your ESP32-C6. Press Enter. **Note**: if this is the first time you are uploading ESPHome to your ESP32-C6, PlatformIO will start downloading the platform packages. By default, the board file for *esp32-c6-devkitc-1* does not accept uploading code using the Arduino framework. The compiler will give the following error: `Error: This board doesn't support arduino framework!`. You will have to do the following:
    - Navigate to 
        - `%USERPROFILE%\.platformio\platforms\espressif32\boards` on Windows.
        - `~/.platformio/platforms/espressif32/boards` on Linux.
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
	    "variant": "esp32c6"
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

<a href="https://www.buymeacoffee.com/immrmkw" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>

