# Flash ROM Manifest

Hello all, this is my ROM primarily for the Nexus 6P (angler) but also buildale for the Nexus 6 (shamu). I will not be sharing this publicly (and I expect you not to as well, see below) but here is how to build it.

## Configure your Linux environment for building

Use my guide [here](https://github.com/nathanchance/Android-Tools/blob/master/Guides/Building_AOSP.txt) for this. I compile on Arch myself so if you need help with setting that up, ask.

## Sync down the repo

```
mkdir <working_dir>
cd <working_dir>
repo init -u https://github.com/Flash-ROM/manifest.git -b n7.1.1
repo sync --force-sync
```

## Set up the build environment 

```
source build/envsetup.sh
```

## Start building 

```
breakfast <device>
mka bacon
```
If all goes well, you will have a zip in out/target/product/<device> when it's done!

## Configuring options

+ `export HAS_GAPPS=false`: Do not build Open GApps into the ROM zip
+ `export HAS_SUBSTRATUM=false`: Do not include a Substratum prebuilt
+ `export HAS_ROOT=false`: Do not include root (Magisk)
+ `export HAS_ROUNDICONS=true`: Include the round icons APK (only needed if building with GApps)

## Some notes

1. I do not give anyone permission to share their builds to a site like XDA or Devs-Base. If you do so, I will have it removed in accordance with their rules. I also do not give anyone permission to use this as a base for their own ROM.
2. I do not provide any support for this. If you build or someone gives you a build, you will receive no assistance from me. If something isn't working, it's most likely something I will fix in due time and if not, it's something with your setup. This is something I do in my free time for me outside of the constraints of users and this is tailored for me, nobody else, which is why it isn't being released publicly.
3. Please do not ask me for builds, I will just ignore the PMs.

I apologize if this sounds overly aggressive but I do what I do for me, nobody else.

## Toolchain issues

I compile my own toolchains from source and because my OS (Arch Linux) may be different from yours, you may run into some errors. Here's how to fix them.

Step 1. Run these commands starting at the head of the source folder:
```
cd .repo
mkdir local_manifests
cd local_manifests
touch toolchains.xml
```
This will change make an empty file for us to add a local manifest to.

Step 2. Open the manifest file in a text editor or nano and add this to it:
```
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
   <remote  name="bitbucket"
            fetch="https://bitbucket.org/" />

   <remove-project name="external_compiler-rt" />
   <project path="external/compiler-rt" name="UBERROMS/external_compiler-rt" groups="pdk" remote="github" revision="master" />
   <remove-project name="aarch64-linux-android-6.x" />
   <project path="prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-6.x" name="uberroms/aarch64-linux-android-6.x" remote="bitbucket" revision="master" />
   <remove-project name="arm-linux-androideabi-6.x" />
   <project path="prebuilts/gcc/linux-x86/arm/arm-linux-androideabi-6.x" name="uberroms/arm-linux-androideabi-6.x" remote="bitbucket" revision="master" />
   <remove-project name="clang_linux-x86_3.9.1" />
   <project path="prebuilts/clang/host/linux-x86/3.9.1" name="uberroms/clang_linux-x86_3.9.1" remote="bitbucket" revision="master" />
</manifest>
```

Step 3. Force sync and build as normal
```
cd ../..
repo sync --force-sync
```

You will only need to perform a force sync anytime you want to build unless you delete your source directory and start over.
