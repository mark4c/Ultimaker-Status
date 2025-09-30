In our workshop we have a row of Ultimaker 3d printers. It's a bit of a hike from the office above the workshop to check on the status of your prints and pulling up a webpage or Cura to check on the print got a bit tedious so I developed an at-a-glance LED status board using some simple parts and a bit of Home Assistant coding with the help of ChatGPT.

Within Home Assistant I'm using:
* [Ultimaker Integration](https://github.com/jellespijker/home-assistant-ultimaker) available from HACS
* [WLED integration](https://www.home-assistant.io/integrations/wled/)

Microcontroller board such as ESP32 with [WLED](https://kno.wled.ge/) installed. Connect to that board over WiFi and set up the 8x8 LED matrix as a segment. I have one microcontroller with three 8x8 panels for our three Ultimakers (two S5 and one 3).

Home Assistant integration is saved here as a separate yaml file, it will need to be adjusted to suit your own setup. The sensor names for instance will need to match your own. I've only tested with Ultimaker S5 and Ultimaker 3, there could be some oddities with other Ultimaker printers.

### WLED send JSON
Within Home Assistant's `configuration.yaml` add the following, replacing the IP address to match your WLED:
```
rest_command:
  wled_send_json:
    url: "http://192.168.0.42/json"
    method: POST
    headers:
      Content-Type: application/json
    payload: "{{ payload }}"
```
This allows us to send the WLED a payload from within our automation.
