# rt-esp

Docker project for FreeRTOS on ESP-8266

## Requirements 

You must have latest version of docker installed and and a user allowed to play docker command.

## Usage

Build the container:
```
docker build -t esptoolchain:latest .
docker run --device=/dev/ttyUSB0:/dev/ttyUSB0:rwm -it esptoolchain /bin/bash
```

Then, connect the ESP8266 kit and run :
```
cd esp\hello_world
make flash monitor
```

