## Bluetooth plugins

This plugin currently adds support for the [HC-05 Bluetooth module](https://duckduckgo.com/?t=ffsb&q=HC-05+Bluetooth+module.&ia=web).

Configuration:

Add/uncomment `#define BLUETOOTH_ENABLE 2` line in _machine.h_ file and recompile.

Adds settings `$71`, `$377` and `$385`.

It has an auto-configure mode to set the module device name and baud rate.
It also supports automatic switching of the active stream to Bluetooth and back on connect/disconnect.
The grblHAL welcome message will be sent to the Bluetooth stream when a connection is established.

Settings:

`$71` - published device name, default is `grblHAL`.  
`$377` - 0, the module is not configured. 1 - the module is configured.  
`$385` - port \(pin\) to use for the state input. Default is the highest numbered usable free port.  
An interrupt capable pin is required and it has to support interrupts on both going low and high.
Tip: Use the `$pins` and `$pinstate` [commands](https://github.com/grblHAL/core/wiki/Report-extensions#pins) to output information on auxiliary pins to the console.
> [!NOTE]
>  The claimed pin is no longer available for `M62`-`M66` commands.

#### Auto configure

Ensure the `$377` setting is set to `0` \(it can be found in the _Bluetooth_ group if your sender supports grouping of settings\).
Power up the controller and the module while pressing down the AT-mode switch on the module.
This will change the controller baud rate to 38400 and it will then send the AT commands required for configuration.
Reports will be sent to the default com port indicating success or failure. Success is also indicated by `$377` beeing set to `1`. 
After auto configuration is completed cycle power to both the module and the controller to start normal operation.

#### Manual configure

If the module is already configured for correct operation \(baud rate set to 115200 baud\) then automatic switching can be enabled by setting `$377` to `1`.

Dependencies:

A free UART port and a free, interrupt capable \(`A`, `C` or `E` mode\), auxiliary input port connected to the module `STATE` pin.

---
2025-10-04
