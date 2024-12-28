# esphome-serta

An esphome configuration to control a Serta bed with Bluetooth

I have an older project, [mqtt-bed](https://github.com/dennyreiter/mqtt-bed/tree/main), which used a Raspberry Pi zero and Python. I've been wanting to get it working on an ESP32 forever, and finally put some effort into it over the Holiday.

I've only implemented the Serta commands, and not even all of them yet, and used a PoE powered Olimex board as I want it to also be a Bluetooth proxy to use with Bermuda. It should work on a wifi board, as well.

### Bed address
There are numerous ways to get the address for your bed. If you can already control the bed via your phone, check the list of paired bluetooth devices, and find the address for your bed's connection in the format `00:00:00:00:00:00`. 

If you have a Serta bed, and are using the [Serta MP Remote app](https://apk-dl.com/serta-mp-remote/), you can find the mac address there.

Using your phone, you can use an app such as [LightBlue](https://punchthrough.com/resources/#lightblue) or another BLE sniffer to find a device starting with `base-i4`.

Otherwise, you can use `hcitool` from the `bluez` package to find the address of your bed:

```console
$ hcitool lescan
LE Scan ...
61:61:61:4E:A0:B0 (unknown)
5F:E4:19:C4:13:CC (unknown)
6F:40:F7:4A:8E:23 (unknown)
7C:EC:79:FF:6D:02 (unknown)
7C:EC:79:FF:6D:02 base-i4.00000233
```

Once you have the address for your bed, you will need to fill that into the `bed_mac_address` variable in the ESPhome yaml file.

## Commands

|Name                    |Command           |
|------------------------|------------------|
| Flat Preset            | e5fe1600000008fe |
| ZeroG Preset           | e5fe1600100000f6 |
| TV Preset              | e5fe1600400000c6 |
| Head Up Preset         | e5fe160080000086 |
| Lounge Preset          | e5fe1600200000e6 |
| Massage Head Add       | e5fe1600080000fe |
| Massage Head Min       | e5fe160000800086 |
| Massage Foot Add       | e5fe160004000002 |
| Massage Foot Min       | e5fe160000000105 |
| Head & Foot Massage On | e5fe160001000005 |
| Massage Timer          | e5fe160002000004 |
| Lift Head              | e5fe160100000005 |
| Lower Head             | e5fe160200000004 |
| Lift Foot              | e5fe160400000002 |
| Lower Foot             | e5fe1608000000fe |

## Resources
* https://github.com/danisla/iot-bed
* https://www.jaredwolff.com/get-started-with-bluetooth-low-energy/

I also took inspiration from this HA Community post:
[Building a integration for a Bluetooth Low Energy (BLE) adjustable bed](https://community.home-assistant.io/t/building-a-integration-for-a-bluetooth-low-energy-ble-adjustable-bed/506812/17)
