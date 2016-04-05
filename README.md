# My kids driving habits

Ever wonder if your kid is a good driver? If they are too hard on the brakes, too heavy on the accelerator or have a habit of tailgating? You can now remotely monitor these habits with the Electron along with the Asset tracker shield and a distance measurement sensor.

A few of the auto-insurance companies now offer a discount by giving you a device which plugs into you car's OBD port that monitors some of these habits (braking and acceleration) but the data belongs to them and it's only for a short duration. This project gives YOU the ownership of that data and allows you to monitor more than just braking and acceleration. Note: It Does not rely on the OBD port though - future revisions could include that.

### Things you'll need:

 - Particle Electron
 - Particle asset tracker shield
 - Sharp distance measurement sensor (GP2Y0A710K0F)
 - External GPS antenna along with SMA to uFL cable and adaptor
 - External cellular antenna
 - LiPo Battery (comes along with the Electron)

The asset tracker shield comes with a weatherproof enclosure. I decided to drill two holes for the SMA connectors; one for the GSM antenna and the other for the Cellular antenna. You can add epoxy around the connectors to make them rain-proof. The accelerometer on-board the asset tracker shield is used to measure braking and accelerations while the GPS measures the location, distance traveled and motion. To monitor the distance from the front of the car, we are using the Sharp GP2Y0A710K0F which can measure distance of up to 5.5 meters.

The whole thing was bolted on to the bumper of my old Subaru. I'm sure there are cleaner and non-intrusive ways of doing this. I was more eager to capture the data than finding an elegant mounting solution.

### Setup:

The asset tracker shield takes care of the connections to the GPS and the accelerometer. The connections to the sensor are very straight forward:

```
Sensor_OUT (White wire) -- Electron_A0
Sensor_PWR (Red Wire) -- Electron_3V3
Sensor_GND (Back wire) -- Electron_GND
```

### Compiling the code:

The project uses the Particle's asset tracker library. Since Electron is a data sensitive device, this example assumes offline development. Here is a link to how to compile and flash your source code locally to the Electron. 

Checkout the develop branch of the Particle firmware repository and create a new folder under firmware/user/applications/. Let us name it driving-habits. Download the code from github into this folder. Now navigate to firmware/modules and use the following command to rebuild your code base:

(this command assumes you are in the develop branch on the particle firmware repository.)

```bash
make clean all PLATFORM=electron APP=driving-habits DEBUG_BUILD=y DEBUG=1 PARTICLE_DEVELOP=1 program-dfu
Note: Before executing the above command, make sure your Electron is in DFU mode and connected to your computer!
```

This command will rebuild the entire source code and flash the binaries in three chunks, system part 1, system part 2 and the user app. In subsequent builds, you don't have to recompile everything. Simply navigate to firmware/main and use the same command - this will only flash the user app binary.
