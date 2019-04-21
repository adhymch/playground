# Setup Dart in your Mac
This article will explain to you how to setup Dartlang and run your first Dart project in MacOS
## 1. Install Dart SDK
Install homebrew, and then run:
```
$ brew tap dart-lang/dart
$ brew install dart
```
Alternatively you can install dev channel release using:
```
$ brew install dart --devel
```
You can always switch from currently active dev channel version to the stable one using:
```
$ brew unlink dart
$ brew install dart
```
When new Dart version is available you can upgrade using:
```
$ brew upgrade dart
```
And to upgrade to a dev channel release when a stable release is currently active, using:
```
$ brew upgrade dart --devel --force
```
You also can switch your Dart version using:
```
$ brew switch dart <dart-version>
```
To check your dart version using:
```
$ brew info dart
```
The command output lists the latest stable and dev versions at the top, followed by your locally installed versions.
## 2. Using IntelliJ IDEA
* Go to this [link](https://www.jetbrains.com/idea/download/#section=mac) to download Intellij IDEA if you don't have one.
* Start the IDE, and install the Dart plugin. To find the Dart plugin, go to Configure > Plugins, then click Install JetBrains plugin, 
and then search 'Dart'. Once you've installed the Dart plugin, restart the IDE.
* Create a new Dart project:
  * From the Welcome screen, click Create New Project.
  * In the next dialog, click Dart.
  * Check **'Generate sample content'** box and choose **console application**
* Write ``` print("hello, world!") ``` in your main class and then run your Dart project.
## 3. Using Visual Studio Code
* Go to this [link](https://code.visualstudio.com/download) to download Visual Studio Code, select Mac.
* Go to extension menu and search for Dart, in the list of resulst install:
  * Dart
  * Pubspec Assist
  * Flutter
* Create new project and then create a pubspec.yaml file (file name shoud be pubspec).
```
name: macsetup
description: this is my first dart app
author: yourname
```
* Create a bin directory by clicking the icon in red box <img width="210" alt="Screen Shot 2019-04-21 at 22 34 00" src="https://user-images.githubusercontent.com/28759060/56472194-a5681300-6485-11e9-8567-f3028698c9bd.png"> to contain your executable files.
In this case create a file name main.dart
```
main(){
  print("hello, world!");
}
```
* Add break point in your main.dart file (in line where you put 'print' syntax) and then press f5 to start the debbug session.


And now you finally run your first app using Dart :)
