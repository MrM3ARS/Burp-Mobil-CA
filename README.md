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
- ADB (Android Debug Bridge) for transferring the module ZIP file.

## Installation

### 1. Export Burp's CA Certificate
1. Open **Burp Suite**.
2. Go to **Proxy** → **Options**.
3. Click **Import / Export CA Certificate**.
4. Select **DER format** and save the certificate as `cacert.der`.

### 2. Convert Certificate to System Format
Android system certificates use a `.0` format with a hashed filename. To convert the certificate:

```sh
openssl x509 -inform DER -in cacert.der -subject_hash_old -noout
```
This will output a hash, e.g., `9a5ba575`.

Rename the certificate accordingly:
```sh
mv cacert.der 9a5ba575.0
```

### 3. Place the Certificate in the Module Directory
Move the converted certificate to the module's system certificate directory inside the repository:
```sh
mv 9a5ba575.0 system/etc/security/cacerts/
```

### 4. Create the Magisk Module ZIP
Once the certificate is placed in the correct directory, navigate to the repository root and package the module into a ZIP file:
```sh
cd <your-magisk-module-repo>
zip -r BurpCA-Magisk-Module.zip .
```

### 5. Transfer the ZIP to Your Device
Instead of using ADB to push the certificate, transfer the module ZIP file directly to your device’s storage (e.g., **SD card, internal storage, or via a file manager**).

### 6. Install the Magisk Module
1. Open **Magisk Manager**.
2. Go to **Modules** and tap **Install from Storage**.
3. Select the module ZIP file and install it.
4. Reboot your device.

### 7. Verify Installation
After reboot, confirm that the certificate is installed:
```sh
ls /system/etc/security/cacerts/ | grep 9a5ba575.0
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
