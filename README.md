# How to Compile an APK in AndroidIDE Using SDK 35 (35.0.0)

This guide will walk you through the process of compiling an APK in AndroidIDE using SDK version 35 (35.0.0). Follow each step carefully to ensure a successful build.

---

## Prerequisites

- **AndroidIDE** installed on your Android device.
- **Internet connection** to download necessary files.

---

## Steps

### **1. Download and Extract the SDK Files**

- **Download the SDK Package**:

  Download the Android SDK for aarch64 from the following link:

  ```
  https://github.com/lzhiyong/termux-ndk/releases/download/android-sdk/android-sdk-aarch64.zip
  ```

- **Create a Directory**:

  Create a folder named `android-sdk-aarch64` in your `Download` directory.

- **Move and Unzip the File**:

  - Move the downloaded ZIP file into the `android-sdk-aarch64` folder.
  - Unzip the file inside this folder.

### **2. Copy Build Tools Version 35.0.0**

- **Open the AndroidIDE Terminal**.

- **Run the Following Command**:

  ```bash
  cp -r /storage/emulated/0/Download/android-sdk-aarch64/android-sdk/build-tools/35.0.0 /data/data/com.itsaky.androidide/files/home/android-sdk/build-tools/
  ```

### **3. Copy Platform Android-35**

- **In the AndroidIDE Terminal**, execute:

  ```bash
  cp -r /storage/emulated/0/Download/android-sdk-aarch64/android-sdk/platforms/android-35 /data/data/com.itsaky.androidide/files/home/android-sdk/platforms/
  ```

### **4. Update the `aapt2` Tool and Organize Folders**

- **Backup Existing `aapt2` (SDK 34)**:

  ```bash
  mkdir -p /data/data/com.itsaky.androidide/files/home/.androidide/34.0.4/
  mv /data/data/com.itsaky.androidide/files/home/.androidide/aapt2 /data/data/com.itsaky.androidide/files/home/.androidide/34.0.4/
  ```

- **Set Up `aapt2` for SDK 35**:

  ```bash
  mkdir -p /data/data/com.itsaky.androidide/files/home/.androidide/35.0.0/
  cp /storage/emulated/0/Download/android-sdk-aarch64/android-sdk/build-tools/35.0.0/aapt2 /data/data/com.itsaky.androidide/files/home/.androidide/35.0.0/
  chmod +x /data/data/com.itsaky.androidide/files/home/.androidide/35.0.0/aapt2
  ```

- **Replace the Existing `aapt2` with the New Version**:

  ```bash
  cp -f /data/data/com.itsaky.androidide/files/home/.androidide/35.0.0/aapt2 /data/data/com.itsaky.androidide/files/home/.androidide/
  ```

### **5. Update Gradle Configuration**

- **Edit `gradle.properties`**:

  Add the following line to suppress the unsupported compile SDK warning:

  ```
  android.suppressUnsupportedCompileSdk=35
  ```

- **Edit `app/build.gradle`**:

  Change the `compileSdk` and `targetSdk` versions to `35`:

  ```gradle
  android {
      compileSdk 35
      ...

      defaultConfig {
          targetSdk 35
          ...
      }
      ...
  }
  ```

---

## Switching Between SDK Versions

If you need to switch back to SDK 34, replace the `aapt2` file with the backed-up version.

- **Run in AndroidIDE Terminal**:

  ```bash
  cp -f /data/data/com.itsaky.androidide/files/home/.androidide/34.0.4/aapt2 /data/data/com.itsaky.androidide/files/home/.androidide/
  ```

---

## Troubleshooting Common Errors

### **1. License Agreement Issues**

If compilation with SDK 35 fails, you might need to accept the SDK licenses.

- **Update Licenses**:

  ```bash
  cd /data/data/com.itsaky.androidide/files/home/android-sdk/cmdline-tools/latest/bin
  ./sdkmanager --licenses
  ```

  Follow the prompts to accept all licenses.

### **2. Gradle Version Compatibility**

If you encounter the following error:

```
> Android resource linking failed
  error: failed to load include path /data/data/com.itsaky.androidide/files/home/android-sdk/platforms/android-35/android.jar.
```

You need to update to a higher version of Gradle.

#### **Update Gradle to Version 8.4**

- **Close the Current Project** in AndroidIDE.

- **Open the AndroidIDE Terminal**.

- **Download and Unzip Gradle 8.4**:

  ```bash
  wget https://services.gradle.org/distributions/gradle-8.4-bin.zip
  unzip gradle-8.4-bin.zip
  rm -rf gradle-8.4-bin.zip
  ```

- **Obtain the Full Path to Gradle**:

  ```bash
  cd gradle-8.4
  pwd
  ```

  Note down the full path displayed (e.g., `/data/data/com.itsaky.androidide/files/home/gradle-8.4`).

- **Configure AndroidIDE to Use the New Gradle Version**:

  - Open **AndroidIDE Settings**.
  - Navigate to **Build Tools > Custom Gradle Installation**.
  - Paste the copied path into the input field.

---

**Note**: After completing these steps, you should be able to compile your APK using SDK 35 successfully.

---

If you have any questions or encounter issues, feel free to ask for assistance.
