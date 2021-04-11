# Flutter setup without android studio

## Table of content

- [Flutter](#Flutter)
- [Requirements](#Requirements)
- [Flutter Setup](#Flutter-Installation)
- [Java Jdk](#Java-Jdk)
- [gragle Setup](#gradle-Setup)
- [Command line tools](#Command-line-tools)
- [Creating Android Virtual Device](#Creating-Android-Virtual-Device-(AVD))
- [Update the path for android SDK](#Update-the-path-for-android-SDK)
- [test Emulator](#Emulator)
- [Vs Code Setup](#Visual-Studio-Code-for-Flutter)

## Flutter

Flutter is Google’s UI toolkit for building beautiful, natively compiled applications for mobile, web, and desktop from a single codebase.

## Requirements

Operating System: Windows 7 or later, x86-64\
Disk Space: 1.6 GB\
Tools: Windows PowerShell, **Git** (Recommend)

You will need

- [flutter sdk](https://storage.googleapis.com/flutter_infra/releases/stable/windows/flutter_windows_2.0.4-stable.zip)
- [Git](https://git-scm.com/)
- [Visual Studio Code](https://code.visualstudio.com/docs/?dv=win64user)
- [JDK 8](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)
- [gradle](https://gradle.org/next-steps/?version=7.0&format=bin) --not necessary(install to be on safe side)
- [Command Line Tools](https://dl.google.com/android/repository/commandlinetools-win-6858069_latest.zip)

## Flutter Installation

choose a directory
> :warning:
>Do not install Flutter in a directory like __C:\Program Files\\@__ that requires elevated privileges

```bash
 git clone https://github.com/flutter/flutter.git -b stable
```

## Update your Path

Steps to add Flutter to the __PATH__ environment variable:

- Open **Edit environment variables for your account.**
  - Under **User Variable** double click *Path*
  - Add flutter bin path in my case **D:\Development\flutter\bin** ok ok done

*confirm by `where flutter dart` command*

## Run `flutter doctor`

from git bash or powershell run `flutter doctor`

```powershell
PS D:\Development\flutter> flutter doctor
Doctor summary (to see all details, run flutter doctor -v):
[√] Flutter (Channel stable, 2.0.4, on Microsoft Windows [Version 10.0.19042.906], locale en-US)
[X] Android toolchain - develop for Android devices
    X Unable to locate Android SDK.
      Install Android Studio from: https://developer.android.com/studio/index.html
      On first launch it will assist you in installing the Android SDK components.
      (or visit https://flutter.dev/docs/get-started/install/windows#android-setup for detailed instructions).
      If the Android SDK has been installed to a custom location, please use
      `flutter config --android-sdk` to update to that location.

[√] Chrome - develop for the web
[!] Android Studio (not installed)
[√] VS Code (version 1.55.1)
```

## Java Jdk

I assume you have setup java home in system variable as **JAVA_HOME** and path to **java/bin**

## gradle Setup

From mobile apps to microservices, from small startups to big enterprises, Gradle helps teams build, automate and deliver better software, faster.

Write in Java, C++, Python or your language of choice. Package for deployment on any platform. Go monorepo or multi-repo. And rely on Gradle's unparalleled versatility to build it all.

Steps to setup gradle:

- Extract `gradle-7.0-bin.zip` zip file
- Move the folder to the desire location in my case `D:\Development\`
- Your directory will look like this:

```bash
D:\
├── Development
│   ├── gradle-7.0
│   │   ├── bin
│   │   ├── init.d
│   │   ├── lib
│   │   ├── LICENSES
│   │   ├── NOTICE
│   │   └── README
│   ├── android_sdk
│   ├── flutter 
```

Update the path:

- Open **Environment Variables**
  - Under **System Variable** Select New..., type

    ```cmd
    Variable name: GRADLE_HOME
    Variable value: D:\Development\gradle-7.0
    ```

  - Under **System Variables** select **Path**, then click Edit. Add an entry for *D:\Development\gradle-7.0\bin*. Click OK to save.

  - Verify your installation by `gradle -v` in the terminal

## Command line tools

If you do not need Android Studio, you can download the basic Android command line tools. You can use the included sdkmanager to download other SDK packages.

- Extract the `commandlinetools-win-6858069_latest.zip`

  - You will get `cmdline-tools` rename it to `tools` thats it
  - Now create another empty folder name it `cmdline-tools` & move the renamed `tools` to `cmdline-tools`
  - Move `cmdline-tools` to a desire directory `android_sdk` in my case: *D:\Development\android_sdk\**
  - Now the directory will look like

```bash
D:\
├── Development
│   ├── android_sdk
│   │   └── cmdline-tools
│   │       └── tools
│   │           ├── bin
│   │           ├── lib
│   │           ├── NOTICE.txt
│   │           └── source.properties
│   │    
│   ├── flutter 
```

- Go to **android_sdk\cmdline-tools\tools\bin\*** you will see some of the *bat* file...
  - Open cmd or powershell in that location by **shift+click** or by file option,..etc

To install the latest platform tools (which includes adb and fastboot) and the SDK, systemimages

in `cmd` or `shell` run the below command:

```cmd
sdkmanager "platforms;android-29"
```

```cmd
sdkmanager "build-tools;29.0.3"
```

*Accept the sdk licenses by `y`*

## List all the system-images and packages

```cmd
sdkmanager --list
```

select any *system-images* you like and install it using the command:

```cmd
sdkmanager "system-images;android-29;default;x86_64"
```

*Accept the licenses by `sdkmanager --licenses`*

## Creating Android Virtual Device (AVD)

 :smile:*key-points to remember*

`-n` : name of the virtual device.
`-k` : image to use, installed above step.
`-d` : device id for hardware profile.

To check device id type `avdmanager.bat list` in the same directory **android_sdk\cmdline-tools\tools\bin** (in the same directory because we still didn't set the bin path to environment variabale yet....)

Create AVD by the command:

```cmd
avdmanager create avd -n Pixel -k 'system-images;android-29;default;x86_64' -d 17
```

DONE...

- Your directory will look like:

```bash
D:\
├── Development
│   ├── android_sdk
│   │   ├── .temp
│   │   ├── build-tools
│   │   ├── cmdline-tools (this was the first file with tools/bin inside)
│   │   ├── emulator
│   │   ├── extras
│   │   ├── licenses
│   │   ├── patcher
│   │   ├── platforms
│   │   ├── platform-tools
│   │   ├── sources
│   │   ├── system-images
│   │   ├── tools
│   │   └── .knowPackages
│   │    
│   ├── flutter 
```

## Update the path for android SDK

DOCUMENTATION *According to google officials*

 **ANDROID_HOME**, which also points to the SDK installation directory, is deprecated.\
 If you continue to use it, the following rules apply:

- If **ANDROID_HOME** is defined and contains a valid SDK installation, its value is used instead of the value in ANDROID_SDK_ROOT.
- If **ANDROID_HOME** is not defined, the value in **ANDROID_SDK_ROOT** is used.
- If **ANDROID_HOME** is defined but does not exist or does not contain a valid SDK installation, the value in **ANDROID_SDK_ROOT** is used instead.

Environment variable :

- Open **Edit environment variables for your account.**
  - Under **System Variable** click **New...**

  ```cmd
  Variable name:  ANDROID_HOME
  Variable value: D:\Development\android_sdk
  ```

  - Again for sdk root

  ```cmd
  Variable name:  ANDROID_SDK_ROOT
  Variable value: D:\Development\android_sdk
  ```

  - Under **System Variable** click **Path** & add (Has to be the same order emulator, tools, platform-tools)
    - %ANDROID_SDK_ROOT%\cmdline-tools\tools\bin
    - %ANDROID_HOME%\emulator
    - %ANDROID_HOME%\tools
    - %ANDROID_HOME%\platform-tools
  
ALMOST DONE

## Emulator

list all the available AVD by the command `emulator -list-avds`

To run the emulator type `emulator -avd avd_pame` or `emulator @avd_name` replace avd_name with the name you gave during Create AVD step in this case **Pixel**

## This is it

From cmd run `flutter doctor -v` later `flutter doctor --android-licenses`

DONE....

## Visual Studio Code for Flutter

- After installation of Vs Code install some the extension for code formating and intellisense
- Open Extensions tab manually or `Ctrl + Shift + x` install the extensions: they are
  - Dart (dart-code.dart-code)
  - Flutter (dart-code.flutter)
  - For More Developer feel :)
    - Bracket Pair Colorizer
    - Image Preview
    - Flutter Widget Snippets
    - Pubspec Assist
- Reload by `Ctrl + Shift + p` type reload click `Reload Window`

Creting flutter application in vs code there are two method:

- Using Vs code GUI
  - Open the Command Palette (Ctrl+Shift+P (Cmd+Shift+P on macOS)).
  - Select the Flutter: New Application Project command and press Enter.
  - Enter your desired Project name.
  - Select a Project location.
  - Then `Ctrl + Shift + p` type flutter launch emulator
  - flutter run form View -> command palette or `Ctrl + Shift + p`

- Using Vs code integrated termainl:
  - Open termianl in vs code by **Ctrl + Shift + `** (control, shift, backtick)
  - Type `flutter create project_name` later `cd project_name`
  - Start the emulator [Emulator](#Emulator) remember the command
  - last `flutter run`
