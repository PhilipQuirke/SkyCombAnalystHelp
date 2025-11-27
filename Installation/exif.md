# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) Installing the ExIf Tool

## Overview
The Exif tool is required to extract metadata from images when processing image files in SkyComb Analyst. This page details how to install it

## Purpose
If you are processing images, you will need the [ExifTool](https://exiftool.org/) to extract metadata from the images. Some of this metadata is encrypted and is not visible using standard Windows image viewers. Exif understands and if necessary decrypts the metadata formats used in many drone images. The encrypted data includes the "raw" radiometric temperature values that SkyComb Analyst needs to detect animals.

## Installation
The latest version of ExIf tool is available at https://exiftool.org

But for Windows users, an easier installer tool for Exif is available at https://oliverbetz.de/pages/Artikel/ExifTool-for-Windows. Download and run the latest "Windows Installer, 64 bit version" 

## Path
The tool needs to be available in your system PATH for SkyComb Analyst to find and use it.

To add ExifTool to your system PATH on Windows:
1. Open the Start Menu and search for "Environment Variables".
2. Click on "Edit the system environment variables".
3. In the System Properties window, click on the "Environment Variables" button.
4. In the Environment Variables window, under the "System variables" section, find and select the "Path" variable, then click "Edit".
5. In the Edit Environment Variable window, click "New" and add the path to the directory where ExifTool is installed (e.g., `C:\Program Files\ExifTool`).
6. Click "OK" to close all windows. 

To test that the ExifTool is correctly installed and available in your PATH:
1. Open a Command Prompt window.
2. Type `exiftool -ver` and press Enter.
3. You should see the version number of ExifTool displayed, indicating that it is correctly installed and accessible.
