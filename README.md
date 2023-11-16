# Pepper Android Emulator Setup

This is a set up guide for configuring your desktop environment to run the Android Studio Pepper emulator. Following the original installation tutorial https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/ch1_gettingstarted/installation.html#installation will result in the Pepper emulator crashing. 

If you are on Ubuntu 22.04, skip step 1 and go straight to application installation.

### Prerequisites
1. Your CPU MUST have the capability to run nested virtualization. Some known issues with this include devices running MacOS with an Intel chip. Check according to your operating system. 
2. A minimum of 50GB of storage space allocated to your VM or your computer if you are on Ubuntu.

## Overview
1. Set up Ubuntu 22.04 VM (Skip if you are on Ubuntu 22.04)
2. Set up Android Studio and Desktop Environment
3. Create Project
4. Run Emulator

## 1. Set up an Ubuntu 22.04 VM

### Windows Hyper-V Set up
Follow this tutorial to create your VM using Hyper-V https://phoenixnap.com/kb/hyper-v-ubuntu
Make sure you are installing Ubuntu 22.04. 

### Other OS VirtualBox Set up
Follow this tutorial to create your VM using VirtualBox https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview
Make sure you are installing Ubuntu 22.04. 

## 2. Set up Android Studio and Desktop Environment

### Download Android Studio
1. From the developer archive, download **Android Studio Bumblebee | 2021.1.1 Patch 3 April 7, 2022** https://developer.android.com/studio/archive
2. Unzip it into Downloads (or wherever you want it to run)
3. Go into the Downloads folder in your terminal and run Android studio using the commands.
```
cd android-studio/bin
./studio.sh
```
4. Install Android studio using the prompts according to default installation settings.
### Install Java 1.8
6. Install Java 1.8 and make sure your system is using Java 1.8. 
```
sudo apt-get install openjdk-8-jdk
java -version
```
### Configure Android Studio Environment for 29.0.3
From Android Studio:

1. Choose Configure > SDK Manager, or
Choose Tools > SDK Manager.
The SDK Manager appears.
2. Checkmark 'Show Package Details'.

3. Select Android API 29 on "SDK Platforms" and click "Apply". The installation should begin.
4. Next to the "SDK Platforms: Tab, there is the "SDK Tools" Tab. Select the tab, checkmark "Show Package Details" and select version 29.0.3. Click the apply button and the installation should begin again.

### Get Pepper SDK Plugin and Tools
1. From Android Studio choose File > Settings, select the Plugins sub-menu.
2. Enter "Pepper" in the search bar. Select "Pepper SDK" and install it.
3. After installation, choose Tools > Pepper SDK > Robot SDK Manager.
4. Select "API 7" and all of the corresponding tools. Click "Apply" and wait until the installation is finished.

### Emulator setup
These instructions are adapted from: https://support.unitedrobotics.group/en/support/discussions/topics/80000657899
1. Install KVM
```
sudo apt install qemu-kvm
```
2. Add yourself to the kvm group
```
sudo adduser yourusername kvm
```
3. Relink the correct libraries

-> 1. Navigate to the API lib folder
   ```
   cd /home/$USER/.local/share/Softbank Robotics/RobotSDK/API 7/tools/lib
   ```
-> 2. Back up the old library
   ```
   mv libz.so.1 libz.so.1.bak
   ```
-> 3. Relink the System one
   ```
   ln -s /usr/lib/x86_64-linux-gnu/libz.so libz.so.1
   ```
4. Restart Android Studio
5. Make sure you can run virtualization by running the following command:
```
 egrep -c '(vmx|svm)' /proc/cpuinfo
```
6. Make sure kvm acceleration is enabled as well:
```
sudo kvm-ok
```
If both these prerequisites are not met, Android Studio will crash if you attempt to run the emulator.

## 3. Create Project
1. From Android Studio, choose: File > New > New Project and configure your project. Minimum API level should be API 23: Android 6.0 (Marshmallow).
2. Configure your project by navigating to File > Project Structure… > Module and make sure Source Compatibility and Target Compatibility are set to 1.8 (Java 8). Also make sure the Compile SDK is 29 and Build Tools version is 29.0.3.
![image](https://github.com/emily-zhang021/PepperAndroidEmulatorSetup/assets/52023695/fc46b3a7-64a9-4c71-a869-046c9b8c58cc)

4. Modify the Gradle JDK to also be 1.8 by going to the same Project Structure window -> SDK Location -> Gradle Settings
![image](https://github.com/emily-zhang021/PepperAndroidEmulatorSetup/assets/52023695/2bbc6822-d30c-4e74-a0c3-f11a6ebb6e36)

6. Restart Android Studio and open your project. Choose File -> New -> Robot Application to robotify your current project.
7. Depending on your language (Kotlin or Java) copy the code snippet from [step 4](https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/ch1_gettingstarted/starting_project.html) into your MainActivity class.
8. You will get errors on the QI SDK libraries that are not imported. Resolve the import errors by hovering over the code and clicking "Resolve".


## 4. Run Emulator
1. Choose Tools > Pepper SDK > Emulator
-> You may get this error:  File Not found "/home/user/Downloads/android-studio/jre/emulator/qemu/linux-x86_64/qemu-system-i386"
   Run this to find the directory location:
   ```
   find qemu
   ```
   For example, mine was in ./Android/Sdk/emulator/qemu. Copy the entire "qemu" folder and place it into wherever your emulator path is. Mine was "/home/user/Downloads/android-studio/jre/emulator"
   Restart Android Studio and try running the emulator again.
   
## 5. Run Project
Once your emulator is running, make sure that: the selected run configuration of your project is app and that the selected device is unknown AOSP on IA Emulator. Click the "Run" button. 
![image](https://github.com/emily-zhang021/PepperAndroidEmulatorSetup/assets/52023695/0a658967-2cc1-4af2-8b90-f2c2a56c32c6)

