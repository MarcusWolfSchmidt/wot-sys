# Conveyor Belt

![ConveyorBelt](Devices/Stepper_Motor_Conveyor_Belt/Images/ConveyorBelt.png)

The conveyor belt is moved by a stepper motor, which is controlled by a Raspberry Pi over a A4988 stepper motor driver. You can find more information about the nodejs library for the A4988 after the Raspberry Pi Configuration. 

## Exposed Thing implementation based on: Exposed Thing with node-wot as Dependency
![Exposed Thing with node-wot as Dependency](https://github.com/eclipse/thingweb.node-wot/tree/master/examples/templates/exposed-thing)

### Raspberry Pi Configuration

You can find more information about the following steps here:  
* [![gpiozero - remote_gpio](https://gpiozero.readthedocs.io/en/stable/remote_gpio.html)](https://gpiozero.readthedocs.io/en/stable/remote_gpio.html)   
* [![npmjs - pigpio](https://www.npmjs.com/package/pigpio)](https://www.npmjs.com/package/pigpio)

```
1)  npm install
2)  (npm install pigpio) -> already included in package.json
3)  Raspberry Pi Configuration -> Enable remote connections -> Remote GPIO: enable
4)  npm run build
5)  instead of npm run start -> sudo npm run start
```
In case of some problems with sudo npm run start, try:
```
sudo shutdown -r 0 
```
and wait until the rpi is ready. 


# A4988
Use an A4988 stepper motor controller on a Raspberry Pi with node.js

You can find more about the original files here:
[![github - A4988](https://github.com/echicken/A4988)](https://github.com/echicken/A4988)

```javascript
const A4988 = require('A4988');
const a4988 = new A4988({ step: 6, dir: 5 });
```

### Constructor

```javascript
new A4988({ step: 26, dir: 19, ms1: 13, ms2: 6, ms3: 5, enable: 22 }); // ms1, ms2, ms3, and enable are optional
```

All parameters are BCM GPIO pin numbers wired to the corresponding A4988 pins.

The _ms1_, _ms2_, and _ms3_ parameters are optional, but required if you want microstepping (_step_size_ below).

### Properties

* **direction** - _boolean_ - Clockwise or counterclockwise, depending on wiring
* **delay** - _number_ - Milliseconds between steps (pulses) (default is 1)
* **step_size** - _string_ - 'full', 'half', 'quarter', 'eighth', or 'sixteenth'
    * ms1, ms2, and ms3 must be wired up and provided to constructor
* **enabled** - _boolean_ - Enable or disable the controller. Set 'true' to enable (default), 'false' to disable. This is at odds with how the pin actually works (active-low) but is clearer.

### Methods

* **turn(1 _[, callback]_)** - Will fire _callback_ when turn is complete (or aborted).  If _callback_ not given, returns a Promise
* **turn_step_size(tss)** - tss = step_size-sting-format like above
* **turn_speed(s)** - s = delay-number-format like above
* **turn_direction(td)** - td = direction-boolean-format like above
* **stop()** - Abort a turn in progress
* **enable()** - boolean-format like above
* **disable()** - boolean-format like above

### Autostart execution Raspberry Pi

Use the following terminal command:
```
crontab -e
```
Write the commands that need to be executed at the reboot of the Raspberry Pi.
Example text:

```
@reboot sleep 10 && ~/Desktop/FolderOfTheThingProgram && npm run start
```
Save and close.

### Schematics

![wiring](Devices/Stepper_Motor_Conveyor_Belt/Schematics/Schematics_Stepper_Motor.png)

![A4988](Devices/Stepper_Motor_Conveyor_Belt/Schematics/A4988_Stepper_Motor_Driver.png)






