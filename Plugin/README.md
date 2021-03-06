# Building the native plugin

It is easier to use the prebuilt binaries included in the test project. However, should you need to build your own native plugin, use these instructions.

## Building the plugin for Windows

Solution and Project files are included for Visual Studio 2015 (works with the Free Community Edition). Just open and build.
Make sure the latest GStreamer 1.x is installed (http://gstreamer.freedesktop.org/data/pkg/windows/) and the
GSTREAMER_1_0_ROOT_X86 or GSTREAMER_1_0_ROOT_X86_64 environment variable is defined and points to the proper place.
The project already copies the resulting GstUnityBridge.dll to the Unity\Assets\Plugins\x86 or x86_64 folder of the included Unity project.

## Building the plugin for Android

Follow the instructions allocated in GUB/Project/Android.


## Building the plugin for Linux

Install dependencies

```sh
# See https://gstreamer.freedesktop.org/documentation/installing/on-linux.html
sudo apt install libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio

# Install gstreamer development packages (headers)
sudo apt install libgstreamer-plugins-base1.0-dev libgstreamer-plugins-good1.0-dev libgstreamer-plugins-bad1.0-dev 
# In other words, the packages that provide the headers for libs listed in the Makefile (Plugin/GUB/Project/Linux/Makefile):
# gstreamer-plugins-base-1.0 gstreamer-app-1.0 gstreamer-video-1.0 gstreamer-net-1.0 gstreamer-pbutils-1.0 gstreamer-gl-1.0

# OpenGL related
sudo apt install freeglut3-dev libglew2.0 libglew-dev libglu1-mesa libglu1-mesa-dev libgl1-mesa-glx libgl1-mesa-dev
```

Build

```sh
cd Plugin/GUB/Project/Linux
make
```

Install

```sh
# Copy the contents of Assets/ to your Unity project's Assets/ folder
cp -r Unity/Assets/* MyPlugin/Assets/

# Copy the plugin library to your Unity project
cp Plugin/GUB/Build/Linux/libGstUnityBridge.so MyPlugin/Assets/Plugins/x86_64/
```

Now in Unity's Project view, select `libGstUnityBridge.so`, uncheck 'Any Platform', and under 'Platform settings' make sure that only 'Linux' and 'x86_64' are checked