# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) Installing the ExIf Tool

## Overview
The Exif tool is required to extract metadata from images when processing image files in SkyComb Analyst. This page details how to install it

## Purpose
If you are processing images, you will need the [ExifTool](https://exiftool.org/) to extract metadata from the images. Some of this metadata is encrypted and is not visible using standard Windows image viewers. Exif understands and if necessary decrypts the metadata formats used in many drone images. The encrypted data includes the "raw" radiometric temperature values that SkyComb Analyst needs to detect animals.

## Installation
The latest version of ExIf tool is available at https://exiftool.org

But for Windows users, an easier installer tool for Exif is available at https://oliverbetz.de/pages/Artikel/ExifTool-for-Windows. Download and run the latest "Windows Installer, 64 bit version" 

The installer has an option “Add EXif tool to path”. Ensure this option is checked during installation.

## Installation Verification
To test that the ExifTool is correctly installed and available in your PATH:
1. Open a Command Prompt window.
2. Type `exiftool -ver` and press Enter.
3. You should see the version number of ExifTool displayed, indicating that it is correctly installed and accessible.

If this doesnt work, try restarting your computer to ensure the PATH changes take effect. If it still doesn't work, you may need to manually add the ExifTool installation directory to your system's PATH environment variable.
