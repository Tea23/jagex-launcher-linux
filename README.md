# Jagex launcher for Linux

This repo contains step by step instruction on how to run the Jagex Launcher in linux as well as how to play through RuneLite

## Disclaimer

I am not affiliated with Jagex or RuneLite, and assumes no responsibility for the contens of this page

## Requirements

- [Wine](https://www.gloriouseggroll.tv/how-to-get-out-of-wine-dependency-hell)
- [WineTricks](https://github.com/Winetricks/winetricks)
- [Jagex Launcher for Windows](https://www.jagex.com/en-GB/launcher)
- [RuneLite for Linux (optional)](https://runelite.net)
- .NET Framework 4.8
- Windows Virtual Machine or Windows computer
<br>

> **Note**
> Anywhere it says USERNAME in all caps needs to replaced with the name of your linux user

## Wine

Click the link under requirements and follow the instructions for your distribution<br>

## WineTricks
Open a terminal and install it through your packet manager<br>
E.g. `sudo apt install winetricks`

## .NET Framework

Open a terminal and type the following command:<br>
`winetricks --force -q dotnet48`

<details>
<summary>Manual installation (Click to expand)</summary><br>

Open a terminal and start Winetricks with following command: `winetricks --force`<br>
Ignore any errors in this step and keep pressing OK until you can proceed

Select "Select the default wineprefix and click OK"<br>
<img src="/assets/images/wineprefix.png"><br>

Select "Install a Windows DLL or component and click OK"<br>
<img src="/assets/images/component.png"><br>

Select "dotnet48" and click OK
<img src="/assets/images/dotnet48.png"><br>

Accept the license terms and click Install<br>
<img src="/assets/images/dotnet4setup.png">

If you get this warning just click Continue<br>
<img src="/assets/images/dotnetwarning.png"><br>

Accept the license terms and click Install<br>
<img src="/assets/images/dotnet4.8setup.png">

</details>

## Jagex Launcher
Install the Jagex Launcher either in a Windows virtual machine or on a seperate computer<br>
Copy the installation folder to your home directory on your Linux computer<br>
Open a terminal, navigate to the Jagex Launcher and start it with the following command: `wine JagexLauncher.exe`

## Desktop entry
Create a new file called `jagex-launcher.desktop` with the following text:
```
[Desktop Entry]
Type=Application
Name=Jagex Launcher
Terminal=false
Exec=wine /home/USERNAME/JagexLauncher/JagexLauncher.exe
Icon=/home/USERNAME/JagexLauncher/Jagex_Launcher_icon.webp
```

Save the file in: `/home/USERNAME/.local/share/appliations`<br>
Download the [Jagex Launcher icon](https://oldschool.runescape.wiki/images/Jagex_Launcher_icon.png) and place it in the same folder as Jagex Launcher<br>
Make sure that the exec path and icon path is the same as the path to the Jagex Launcher<br>

## RuneLite

Navigate to this directory: `/home/USERNAME/.wine/drive_c/users/USERNAME/AppData/Local` and create a new folder called `RuneLite`<br>
Copy `RuneLite.AppImage` to the folder and make it executable with the following command: `sudo chmod +x RuneLite.AppImage`<br>
Create a new file called `RuneLite.sh` with the following text:
```
#!/bin/sh
cd /home/USERNAME/.wine/drive_c/users/USERNAME/AppData/Local/RuneLite
./RuneLite.AppImage
```
Make `RuneLite.sh` executable with the following command: `sudo chmod +x RuneLite.sh`<br>
Create a symbolic link to RuneLite.sh with the following command: `ln -s RuneLite.sh RuneLite.exe`

## Windows Registry

Create a new file called `InstallLocation.reg` with the following text:
```
Windows Registry Editor Version 5.00
[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Uninstall\RuneLite Launcher_is1]
"InstallLocation"="/home/USERNAME/.wine/drive_c/users/USERNAME/AppData/Local/RuneLite"
```
Save the file in your home directory<br>
Open Windows Registry Editor with the following command: `winetricks --force regedit`<br>
Select registry, Import Registry File.. and import the file you just created.

<details>
<summary>Once you are done it should look like this (Click to show image)</summary><br>
<img src="/assets/images/regedit.png">
</details>
<br>

Open the Jagex launcher with your new desktop entry. If everything is done correctly it should say play when selecting RuneLite from the client drop down menu.

# Credits

Thanks to c00k and jolty__ for making the information available to create this repo

How to use Jagex's New Launcher on Linux [by c00k](https://youtu.be/izLxF_Wwinw)
<br>
Native Linux RuneLite running with Jagex Launcher [by jolty__](https://www.reddit.com/r/2007scape/comments/uo1ey1/native_linux_runelite_running_with_jagex_launcher)

