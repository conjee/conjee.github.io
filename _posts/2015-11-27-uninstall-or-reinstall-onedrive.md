---
title: How to Uninstall or Reinstall OneDrive in Windows 10
categories: 
  - Tricks
tags: 
  - OneDrive
  - Windows 10
published: true
excerpt: Solve annoying problems related to OneDrive by uninstalling or reinstalling it in Windows 10
---
Windows 10 integrates OneDrive Service by default. However, it's annoying for users who don't use Onedrive:

1. Runs at startup
2. Pinned at the left panel in File Explorer
3. Appears in Open/Save dialog boxes
4. Error prompts

To fix 1, you can disable OneDrive in Task Manager - Startup. [Uninstalling OneDrive](#how-to-uninstall) can fix 1, 3 and 4. To fix 2, you need to [edit Registry](#edit-registry-to-remove-onedrive-entry-from-file-explorer). If you do use OneDrive and want to fix error prompts, you can try [reinstalling OneDrive](#uninstallreinstall-onedrive).

#### Uninstall/Reinstall OneDrive

##### How to uninstall

1. Right-click on the Windows icon on your taskbar and choose `Command Prompt (Admin)`
2. Enter `taskkill /f /im OneDrive.exe` to kill OneDrive process if it's running
3. Run `%SystemRoot%\System32\OneDriveSetup.exe /uninstall` if you have a 32-bit system or `%SystemRoot%\SysWOW64\OneDriveSetup.exe /uninstall` if you have a 64-bit system

You won't see any feedback message, but OneDrive is uninstalled.

##### How to reinstall

Run the proper Setup Program:

`%SystemRoot%\System32\OneDriveSetup.exe` in a 32-bit system and

`%SystemRoot%\SysWOW64\OneDriveSetup.exe` in a 64-bit system.

#### Edit Registry to remove OneDrive entry from File Explorer

1. Right-Click on the Windows icon on your task bar and choose `Run`
2. Enter `regedit` to open Registry Editor
3. Navigate to `HKEY_CLASSES_ROOT\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}` Note: You can search (shortcut: `Ctrl + F`) for `{018D5C66-4533-4307-9B53-224DE2ED1FE6}`
4. Change the value of `System.IsPinnedToNameSpaceTree` to `0`

OneDrive entry should disappear from your File Explorer now. To restore, Change the value back to `1`.
