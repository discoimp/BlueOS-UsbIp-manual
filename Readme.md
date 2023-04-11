### See parent repos for original description.
The service did not function correctly, so I will write down an alternative method here given you are able to find the busid of the device you want to connect to.

Test it first, and then add it to the startup script.

# On the BlueOS device running beta version BlueOS (minimum 1.1.0-beta.16)
navigate to add ons and install docker usbip or VirtualHere


# On the BlueOS device running release version BlueOS


On the BlueOS device, run the following command:

```
red-pill
sudo apt update && sudo apt install usbip hwdata usbutils
sudo modprobe usbip-core && sudo modprobe usbip-host
usbip list -l

```
Find the device you want to connect to, and note the busid. In the example below, the busid is 1-1.5.

```
sudo usbip bind -b 1-1.5
```
The response should be something like:

```
usbip: info: bind device on busid 1-1.5: complete
```
Your client device should now be able to connect to the host device.

# On topside Linux
Run the following command if on Ubuntu 22.04:
```
sudo apt install linux-tools-virtual hwdata linux-t
sudo update-alternatives --install /usr/local/bin/usbip usbip $(command -v ls /usr/lib/linux-tools/*/usbip | tail -n1) 20
sudo apt update && sudo apt install usbip
usbip --help
```
When running the last command usbip will specify a kernel-specific linux-tools-#.##.##.##-##-generic. Install it (check the version number from your output and change the following accordingly:
```
sudo apt install linux-tools-5.15.0-69-generic
```
then run this and you should be good to go:
```
sudo apt install linux-tools-generic canberra-gtk-module
```

# Client

## VirtualHere client
Download the [VirtualHere client](https://www.virtualhere.com/usb_client_software)
In my case (navigate to the folder where you saved your file):
```
chmod +x vhuit64
```
Run with sudo
```
sudo ./vhuit64
```

If your server is running a slim gui will display available devices to connect.

## usbip terminal:


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
