# Pepper Android Emulator Setup

This is a set up guide for configuring your desktop environment to run the Android Studio Pepper emulator. Following the original installation tutorial https://qisdk.softbankrobotics.com/sdk/doc/pepper-sdk/ch1_gettingstarted/installation.html#installation will result in the Pepper emulator crashing. 

Enable virtualization. 

If you are on Ubuntu 22.04, skip step 1 and go straight to application installation.

# Overview
1. Set up Ubuntu 22.04 VM (Skip if you are on Ubuntu 22.04)
2. Set up Android Studio and Desktop Environment
3. Create and run project
  
7. Enable Virtualization/Nested Virtualization
8. Create project

## 1. Set up an Ubuntu 22.04 VM

### Prerequisites
1. Your CPU MUST have the capability to run nested virtualization. Some known issues with this include devices running MacOS with an Intel chip. Check according to your operating system. 
2. A minimum of 50GB of storage space allocated to your VM.
- - - 
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


## 3. Create and Run Project

https://ubuntu.com/download/desktop
