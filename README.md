# Groundlight' Monitoring Notification Server (MNS) as a Raspberry Pi Appliance

This repo builds the OS image for a Groundlight MNS appliance running on Raspberry Pi hardware.

Use this repo to build the `.img` file which gets burned to an SD card.  When that SD card is booted on the Raspberry Pi, 
it runs the Groundlight Monitoring Notification Server.

This build system is based on [pi-gen](https://github.com/RPi-Distro/pi-gen).  Refer to its [original README](PI-GEN-README.md) for how everything works.  But the (`config`)[config] file is the key source of control.

## Building Images

You should really build this on an ARM system (e.g. an m7g instance in ec2).  
You _can_ build this on an x86 instance, but it will take ~3x longer, and it's not fast to start with.

### Building directly

On the appropriate machine, run:

```
time sudo ./build.sh
```

### Building in Docker

If you're not crazy about running this big script as root, you can use:

```
time ./build-docker.sh
```

It's slower (how much?), but still manages to cache previous runs.  The second time you run it
to re-use the cache, you should do:

```
time CONTINUE=1 ./build-docker.sh
```

### Troubleshooting

Add `CLEAN=1` before running the script to start over.

## Using the images

After ~10 minutes, and then look in the `deploy/` for a file with a name like
`image_2023-12-06-GroundlightMNS-sdk-qemu.img.xz` which will be ~1GB for now.
(See the `COMPRESSION_LEVEL` setting in (`config`)[config] to trade speed vs size.)

Copy this to your laptop, and then you can burn it to an SD card using the [Raspberry Pi Image](https://github.com/raspberrypi/rpi-imager).

