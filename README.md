# Flash ROM Manifest

Hello all, this is my ROM for the Nexus 5X (bullhead), 6 (shamu), and 6P (angler). It is based on Pure Nexus with some additional features I have pulled from other ROMs.

I will not be sharing this publicly (and I expect you not to as well, see below) but here is how to build it.

## Configure your Linux environment for building

Use my guide [here](https://github.com/nathanchance/Android-Tools/blob/master/Guides/Building_AOSP.txt) for this. I compile on Arch myself so if you need help with setting that up, ask.

## Sync down the repo

```
mkdir <working_dir>
cd <working_dir>
repo init -u https://github.com/Flash-ROM/manifest.git -b n7.1
repo sync --force-sync
```

## Set up the build environment 

```
source build/envsetup.sh
```

## Start building 

```
breakfast <device_codename>
mka bacon
```
If all goes well, you will have a zip in out/target/product/<device_codename> when it's done!

## Some notes

1. I do not give anyone permission to share their builds to a site like XDA or Devs-Base. If you do so, I will have it removed in accordance with their rules.
2. I do not provide any support for this. If you build or someone gives you a build, you will receive no assistance from me. This is something I do in my free time for me outside of the constraints of users.

I apologize if this sounds overly aggressive but I do what I do for me, nobody else.
