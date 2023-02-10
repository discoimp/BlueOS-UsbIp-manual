### See below for original description.
The service did not function correctly, so I will write down an alternative method here.

# USB/IP extension

This exposes usb devices via IP, which can be used in another client device

To use, first pull it in blueos:


```
red-pill
sudo docker run -d --net=host --name=blueos-example1 --restart=unless-stopped williangalvani/blueos-extension-usbip:latest
```

# Client

## Linux:


```
# load modules
sudo modprobe usbip-core
sudo modprobe vhci-hcd
# list devices
sudo usbip list --remote blueos.local
# connect to device with bus 1-1.3
sudo usbip attach --remote blueos.local --busid 1-1.3

```

## Windows

Download the 3.6 dev release from https://github.com/cezanne/usbip-win and follow the "Client" instructions there.
The new "ude" driver seemed to work for me.
