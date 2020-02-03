# rt-esp

Vagrant project for FreeRTOS on ESP-8266

## Requirements 

You must have latest version of virtualbox installed with the extension pack for USB support and then install the vagrant reload plugin using :
```
vagrant plugin install vagrant-reload
```

## Provisionning the VM

From terminal :
```
vagran up
vagrant ssh
```

Once connected to the vm, connect the ESP8266 kit and run :
```
cd esp\hello_world
make flash monitor
```

