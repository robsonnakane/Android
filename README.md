# Android
Install LineageOS on Motorola one fusion+
liber
Warning: The provided instructions are for LineageOS 19.1. These will only work if you follow every section and step precisely.
Do not continue after something fails!
Basic requirements

    Read through the instructions at least once before actually following them, so as to avoid any problems due to any missed steps!
    Make sure your computer has adb and fastboot. Setup instructions can be found here.
    Enable USB debugging on your device.
    Make sure that your model is actually listed in the “Supported models” section here (exact match required!)
    Boot your device with the stock OS at least once and check every functionality.
    warning
    Warning: Make sure that you can send and receive SMS and place and receive calls (also via WiFi and LTE, if available), otherwise it won’t work on LineageOS either! Additionally, some devices require that VoLTE/VoWiFi be utilized once on stock to provision IMS.
    LineageOS is provided as-is with no warranty. While we attempt to verify everything works you are installing this at your own risk!

warning
Warning: Before following these instructions please ensure that the device is currently using Android 11 firmware.
If the vendor provided multiple updates for that version, e.g. security updates, make sure you are on the latest!
If your current installation is newer or older than Android 11, please upgrade or downgrade to the required version before proceeding (guides can be found on the internet!).
Checking the correct firmware

Installation on your device requires a specific firmware version to be installed before you continue.

    Firmware refers to a device-specific set of images that are included in, and updated by the stock OS
    LineageOS builds for this device require a specific version of the stock OS to be installed prior to following the installation guide
    Please ensure that you are checking the Android version, and not the vendor OS version
    Being on another custom ROM, including unofficial builds of the same version of LineageOS, does not ensure that this requirement has been fulfilled
    Please re-read this section as many times as necessary to fully understand the requirements

info_outline
Note: If you are unsure what firmware version you are currently on, we strongly recommend returning to the corresponding stock OS before following the installation guide!

Failing to install the correct firmware version prior to installation may result in failure to install LineageOS, unexpected crashes post-installation, or permanent damage to your device!
Unlocking the bootloader
info_outline
Note: The steps below only need to be run once per device.
warning
Warning: Unlocking the bootloader will erase all data on your device! Before proceeding, ensure the data you would like to retain is backed up to your PC and/or your Google account, or equivalent. Please note that OEM backup solutions like Samsung and Motorola backup may not be accessible from LineageOS once installed.

    Connect the device to your PC via USB.
    On the computer, open a command prompt (on Windows) or terminal (on Linux or macOS) window, and type:

    adb reboot bootloader

    You can also boot into fastboot mode via a key combination:
        With the device powered off, hold Volume Up + Volume Down + Power.
    Once the device is in fastboot mode, verify your PC finds it by typing:

    fastboot devices

    If you don’t get any output or an error:
        on Windows: make sure the device appears in the device manager without a triangle. Try other drivers until the command above works!
        on Linux or macOS: If you see no permissions fastboot try running fastboot as root. When the output is empty, check your USB cable and port!

    Follow the instructions at Motorola Support to unlock your bootloader.
    info_outline
    Note: Some newer Motorola devices have a waiting period before you can enable OEM Unlock option in the developer options. It can sometimes take up to one week.
    info_outline
    Note: If your device is not supported by the Motorola Bootloader Unlock website, you may be able to use an alternative bootloader unlock method like SunShine, though they only support some devices/firmwares.
    Since the device resets completely, you will need to re-enable USB debugging to continue.

Installing a custom recovery using fastboot

    Download Lineage Recovery. Simply download the latest recovery file, named recovery.img.
    warning
    Important: Other recoveries may not work for installation or updates. We strongly recommend to use the one linked above!
    Connect your device to your PC via USB if it isn’t already.
    If your device isn’t already in fastboot mode, on the computer, open a command prompt (on Windows) or terminal (on Linux or macOS) window, and type:

    adb reboot bootloader

    You can also boot into fastboot mode via a key combination:
        With the device powered off, hold Volume Up + Volume Down + Power.
    Once the device is in fastboot mode, verify your PC finds it by typing:

    fastboot devices

    If you don’t get any output or an error:
        on Windows: make sure the device appears in the device manager without a triangle. Try other drivers until the command above works!
        on Linux or macOS: If you see no permissions fastboot try running fastboot as root. When the output is empty, check your USB cable and port!
    check
    Tip: Some devices have buggy USB support while in bootloader mode, if you see fastboot hanging with no output when using commands such as fastboot getvar ..., fastboot boot ..., fastboot flash ... you may want to try a different USB port (preferably a USB Type-A 2.0 one) or a USB hub.
    Flash recovery onto your device:

    fastboot flash recovery recovery.img

    Now reboot into recovery to verify the installation.
        Use the menu to navigate to and to select the Recovery option.
    info_outline
    Note: If your recovery does not show the LineageOS logo 

    , you accidentally booted into the wrong recovery. Please start at the top of this section!

Ensuring all firmware partitions are consistent
info_outline
Note: The steps below only need to be run once per device.

In some cases, the inactive slot can be unpopulated or contain much older firmware than the active slot, leading to various issues including a potential hard-brick. We can ensure none of that will happen by copying the contents of the active slot to the inactive slot.

To do this, sideload the copy-partitions-20220613-signed.zip package by doing the following:

    Download the copy-partitions-20220613-signed.zip file from here. It should have a MD5 sum of 79f2f860830f023b7030c29bfbea7737 or a SHA-256 sum of 92f03b54dc029e9ca2d68858c14b649974838d73fdb006f9a07a503f2eddd2cd.
    Sideload the copy-partitions-20220613-signed.zip package:
        On the device, select “Apply Update”, then “Apply from ADB” to begin sideload.
        On the host machine, sideload the package using: adb sideload copy-partitions-20220613-signed.zip
    info_outline
    Note: The copy-partitions script was created by LineageOS developer erfanoabdi and filipepferraz
    Now reboot to recovery by tapping “Advanced”, then “Reboot to recovery”.

Installing LineageOS from recovery

    Download the LineageOS installation package that you would like to install or build the package yourself.
        (Optionally): If you want to install an application package add-on such as Google Apps (use the arm64 architecture), please read and follow the instructions on Google Apps page
    If you are not in recovery, reboot into recovery:
        With the device powered off, hold Volume Down + Power.
    Now tap Factory Reset, then Format data / factory reset and continue with the formatting process. This will remove encryption and delete all files stored in the internal storage, as well as format your cache partition (if you have one).
    Return to the main menu.
    Sideload the LineageOS .zip package but do not reboot before you read/followed the rest of the instructions!
        On the device, select “Apply Update”, then “Apply from ADB” to begin sideload.
        On the host machine, sideload the package using: adb sideload filename.zip.
        check
        Tip: Normally, adb will report Total xfer: 1.00x, but in some cases, even if the process succeeds the output will stop at 47% and report adb: failed to read command: Success. In some cases it will report adb: failed to read command: No error or adb: failed to read command: Undefined error: 0 which is also fine.

Installing Add-Ons
info_outline
Note: If you don’t want to install any add-on (such as Google Apps), you can skip this whole section!
warning
Warning: If you want the Google Apps add-on on your device, you must follow this step before booting into LineageOS for the first time!

    Even though you are already in recovery, click Advanced, then Reboot to Recovery

    When your device reboots, click Apply Update, then Apply from ADB, then adb sideload filename.zip for all desired packages in sequence.
    info_outline
    Note: Add-ons aren’t signed with LineageOS’s official key, and therefore when they are sideloaded, Lineage Recovery will present a screen that says Signature verification failed, this is expected, please click Continue.

All set!

Once you have installed everything successfully, you can now reboot your device into the OS for the first time!

    Click the back arrow in the top left of the screen, then “Reboot system now”.

info_outline
Note: The first boot usually takes no longer than 15 minutes, depending on the device. If it takes longer, you may have missed a step, otherwise feel free to get assistance.
