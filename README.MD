# OniVim2 builder image

Builder for [Onivim2](onivim.github.io/) app on Ubuntu 20.04 system.

## OniVim2 development support

I am releasing this image to let you try out and maybe hack on Onivim2 to support its development. 
Yet please consider supporting the project financially: [you can support the project on Patreon or buy a License here](https://v2.onivim.io/early-access-portal).
This is a complex project and needs a lot of work!

## Builder image

This is a docker image which builds Onivim:
- It runs and compiles against Ubunbu 20.04 - the resulting App can be protable to other distributions, provided the libraries have similar versions.
- You will need to have at least 17 GB of free space to build (sic!)
- Prepare a directory where build user will have it's home

To build Onivim2 using image I have built:
```
docker run -it --rm --name onivimbuilder -v $BUILD_DIRECTORY:/home/oni --env TAG=master movonw/onivim2-builder  
```

To build the image yourself from this repository:

```
docker build -t onivim2-builder .  
```

A succesful build ends with:
```
Marking the AppImage as executable...
Embedding MD5 digest
Success

Please consider ....
```

After the build hopefully succeeds you will find AppImage in `$BUILD_DIRECTORY/oni2/_release/Onivim2-x86_64.AppImage`. Just `chmod +x` and run this file.


If nothing happens (the app does not start), you can debug it by running:

```
Onivim2-x86_64.AppImage --appimage-mount
```
it will mount the app image and display a path under `/tmp/.mount_oniXXXXXXX` -> go to this directory, open `usr/bin` and try to run `Oni2_editor -f`, you can also run `ldd Oni2_editor` to see if there are missing dependencies (look for "not found" in the output).

# Installing in system

To install, 
- move the Onivim appimage file to `/usr/local/bin/Oni2`. Also, to get it to show up in app menu and see the beautiful icon:
- put [Onivim2.desktop](https://raw.githubusercontent.com/onivim/oni2/e849d67e8128bab99874bbb988bcf0f940c44262/scripts/linux/Onivim2.desktop) in `/usr/share/applications`
- put [Onivim2.png](https://github.com/onivim/oni2/raw/e849d67e8128bab99874bbb988bcf0f940c44262/assets/images/logo.png) in `/usr/share/icons`


Hope this works for you!

Hit me up on Discord - nickname @MOss.

