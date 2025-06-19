# AOSP Custom Firmware with Gapps (Android 13)

Welcome to the repository for the AOSP custom firmware image (`aosp_cf_x86_64_phone-img-xxxxxx.zip`) built for x86_64 phone emulation with Google Apps (Gapps) included, running Android 13.

## Overview
This project provides a pre-built AOSP image for x86_64 phone emulation, integrated with Gapps to enable Google Play Services and other Google applications out of the box. It is designed for developers, testers, and enthusiasts who want to experiment with Android 13 in an emulated environment.

## Features
- **Base**: Android Open Source Project (AOSP) Android 13
- **Architecture**: x86_64
- **Google Apps**: Pre-installed Gapps for Google Play Store, Gmail, and other Google services
- **Target**: Phone emulation (ideal for Android Virtual Device or similar emulators)

## Prerequisites
Before using this image, ensure you have the following:
- An emulator supporting x86_64 architecture (e.g., Android Studio's AVD Manager)
- Basic knowledge of Android emulation and flashing images
- Sufficient storage space for the image and emulator setup
- Tools like `adb` and `fastboot` installed (included with Android SDK)

## Installation Instructions
1. **Download the Image**:
   - Download `aosp_cf_x86_64_phone-img-xxxxxx.zip` from the [Releases](https://github.com/hipexscape/cuttlefish_releases/releases) section or the repository root.
   - Extract the zip file to obtain the image files.

2. **Set Up Emulator**:
   - Open Android Studio and launch the AVD Manager.
   - Create a new virtual device with x86_64 architecture and Android 13 as the system image.
   - Alternatively, use another emulator that supports custom AOSP images.

3. **Flash the Image**:
   - Replace the default system image in your emulator with the extracted `aosp_cf_x86_64_phone-img-xxxxxx` image.
   - Follow your emulator's documentation for loading custom images

4. **Boot the Emulator**:
   - Start the virtual device in the emulator.
   - The device should boot into Android 13 with Gapps pre-installed.

5. **Verify Gapps**:
   - Open the Play Store and sign in with your Google account to confirm Gapps functionality.

## Known Issues
- Some emulator-specific features (e.g., GPU acceleration) may require additional configuration.
- Gapps performance depends on emulator resources; allocate sufficient RAM and CPU cores.

# Fix for Uncertified Device Warning

If you encounter the "This device isn't Play Protect certified" warning on your AOSP custom firmware (Android 13) with Gapps, follow these steps to register your device ID with Google and resolve the issue:

## Steps to Fix

1. **Download the Device ID App**:
   - Run the cuttlefish using `launch_cvd` command.
   - Download the Device ID app:
     ```
     wget https://github.com/hipexscape/cuttlefish_releases/releases/download/device-id-1-1-3/device-id-1-1-3.apk
     ```
   - Install the app on your device:
     ```
     adb install device-id-1-1-3.apk
     ```

2. **Run the App and Get Device ID**:
   - Open the "Device ID" app on your device.
   - Note down the device ID displayed.

3. **Register Device ID with Google**:
   - Visit [https://www.google.com/android/uncertified/](https://www.google.com/android/uncertified/).
   - Enter the device ID from the app into the provided field.
   - Follow the on-screen instructions to submit and wait for Google to process the request (this may take a few hours).

4. **Clear Play Store Data and Cache**:
   - On your computer, run the following ADB commands to clear Play Store data and cache:
     ```
     adb shell pm clear com.android.vending
     ```
   - Restart your device.

5. **Verify Fix**:
   - Open the Google Play Store app.
   - Sign in with your Google account. The "uncertified device" warning should no longer appear.
