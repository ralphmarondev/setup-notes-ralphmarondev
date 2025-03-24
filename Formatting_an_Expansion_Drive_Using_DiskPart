# Formatting an Expansion Drive Using DiskPart

## Overview
This guide explains how to format an external expansion drive using Windows' built-in **DiskPart** tool without any external software. This method is useful when the drive is not appearing in File Explorer but is detected in **Disk Management**.

## ⚠ Warning
Formatting a drive **will erase all data** on it. Make sure you have selected the correct disk before proceeding.

## Steps to Format the Expansion Drive

### 1. Open Command Prompt as Administrator
- Press `Win + R`, type `cmd`, and press `Ctrl + Shift + Enter` to open Command Prompt with admin privileges.

### 2. Open DiskPart
- Type the following command and press **Enter**:
  ```sh
  diskpart
  ```

### 3. Identify the Expansion Drive
- List all connected disks:
  ```sh
  list disk
  ```
- Identify your external drive by checking its **size**.
  - Example output:
    ```
    Disk ###  Status         Size     Free     Dyn  Gpt
    --------  -------------  -------  -------  ---  ---
    Disk 0    Online          238 GB  1024 KB        *
    Disk 1    Online          931 GB      0 B        *
    Disk 2    Online          931 GB      0 B        *
    ```
- To confirm the drive details, select the disk and check its properties:
  ```sh
  select disk 2  # Replace 2 with your disk number
  detail disk
  ```
  - If it is a **USB drive**, it should mention something like `Seagate Expansion SCSI Disk Device`.

### 4. Clean the Drive
- **Erase all partitions** on the selected disk:
  ```sh
  clean
  ```

### 5. Create a New Partition
- Create a **primary partition**:
  ```sh
  create partition primary
  ```

### 6. Format the Drive
- **For Windows Only (NTFS format)**:
  ```sh
  format fs=ntfs quick
  ```
- **For Windows & macOS Compatibility (exFAT format)**:
  ```sh
  format fs=exfat quick
  ```

### 7. Assign a Drive Letter
- To make the drive visible in **File Explorer**:
  ```sh
  assign
  ```

### 8. Exit DiskPart
- Close the utility:
  ```sh
  exit
  ```

## Verification
- Open **File Explorer** (`Win + E`) and check if the formatted expansion drive is now accessible.
- Try copying files to the drive to ensure it is working correctly.

## Troubleshooting
- If the drive does not appear in File Explorer, go to **Disk Management** (`Win + X → Disk Management`) and check if it has a drive letter assigned.
- If formatting fails, try running `clean` again and restarting the process.

---

**Author:** Guide written based on user experience formatting a Seagate Expansion Drive.

**Last Updated:** March 2025

