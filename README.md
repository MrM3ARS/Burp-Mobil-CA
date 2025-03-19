# Burp CA Magisk Module

## Overview
This Magisk module automates the installation of Burp Suite's CA certificate as a system-wide trusted certificate on Android devices. By using this module, you can bypass Android's certificate restrictions and perform HTTPS traffic interception without manually modifying system files.

## Features
- Automatically installs Burp Suite's CA certificate as a system-trusted CA.
- No need to manually push certificates or modify system partitions.
- Works seamlessly with Android 7+ (including newer Android versions that enforce certificate restrictions).
- Persistent installation – the certificate remains trusted even after reboot.

## Requirements
- Rooted Android device with **Magisk** installed.
- Burp Suite installed on your computer.
- ADB (Android Debug Bridge) for transferring the certificate.

## Installation

### 1. Export Burp's CA Certificate
1. Open **Burp Suite**.
2. Go to **Proxy** → **Options**.
3. Click **Import / Export CA Certificate**.
4. Select **DER format** and save the certificate as `cacert.der`.

### 2. Transfer the Certificate to Your Device
Use ADB to push the certificate to a known location on your device:
```sh
adb push cacert.der /sdcard/
```

### 3. Install the Magisk Module
1. Download the Magisk module from [GitHub](your-repo-link-here).
2. Open **Magisk Manager**.
3. Go to **Modules** and tap **Install from Storage**.
4. Select the module ZIP file and install it.
5. Reboot your device.

### 4. Verify Installation
After reboot, confirm that the certificate is installed:
```sh
ls /system/etc/security/cacerts/ | grep burp
```
If you see a `.0` file with a hash-like name, the installation was successful.

Alternatively, go to **Settings** → **Security** → **Encryption & Credentials** → **Trusted Credentials (System)** and check if Burp's CA is listed.

## Uninstallation
To remove the module:
1. Open **Magisk Manager**.
2. Navigate to **Modules**.
3. Find the Burp CA Magisk module and tap **Remove**.
4. Reboot your device.

## Troubleshooting
- **Certificate not recognized?** Try reinstalling the module and rebooting.
- **Still untrusted?** Ensure your Android version is supported and the module was correctly installed.
- **Module not appearing in Magisk?** Make sure you installed the correct ZIP file and granted Magisk sufficient permissions.

## Disclaimer
This module modifies system files related to security certificates. Use it responsibly and only on devices you control. The author is not responsible for any misuse or damage caused.

## Contributions & Support
Feel free to open an issue or submit a pull request if you encounter any problems or want to improve the module.

---
📌 **GitHub Repository:** [your-repo-link-here]
