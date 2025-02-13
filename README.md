# Pusher Channels Unity Client Library

This library packages [the official WebSocket .NET SDK for Pusher Channels](https://github.com/pusher/pusher-websocket-dotnet) as a `.unitypackage` and an `UPM package` to make it easier to use in [Unity](https://unity.com/) projects. For API documentation, see [the pusher-websocket-dotnet README](https://github.com/pusher/pusher-websocket-dotnet).

## Repository Structure
-  `BaseProject` a Unity Base project which demonstrates how to integrate Pusher Channels with Unity
-  `Builds` a build environment for the `PusherWebsocketUnity` _unitypackage_ and the _Unity Package Manager_ (UPM) release
-  `Examples` example projects that combines Unity and Pusher Channels

## Unity Versions Support

- Unity 2019, 2020, 2021 and 2022

## Getting Started
1. [Create a Pusher Channels app](#1-create-a-pusher-channels-app)
2. [Install](#2-install) the **Pusher Channels Unity Client Library** via `unitypackage` or via Unity Package Manager (UPM)
3. [IL2CPP Extra Steps (Ignore if using Mono)](#3-il2cpp-extra-steps)
4. [Add PusherManager and run the game](#4-add-pushermanager-and-run-the-game)

### 1 Create a Pusher Channels app
1.1 - Create a Pusher Channels app at https://pusher.com/channels

### 2 Install
#### 2.1 Install it via unitypackage
2.1.1 - Download the latest `PusherWebsocketUnity-2.3.0-beta+230104.unitypackage` from [releases](/../../releases)<br>
2.1.2 - Open a new/existing Unity project and make sure it is being opened by a [supported version of Unity](#unity-versions-support)<br>
2.1.3 - [if your Unity version is **2018.x.x**] Make sure that under `Edit -> Project Settings -> Player` the `Configuration -> Scripting Runtime Version` is set to **.NET 4.x Equivalent**.<br>
2.1.4 - Click on `Assets -> Import Package -> Custom Package...`, find and select the `PusherWebsocketUnity-2.3.0-beta+230104.unitypackage` and click *Import* on the `Import Unity Package` window.<br>

#### 2.2 Install it via Unity Package Manager (UPM)
**WARNING** this method works only if your version of Unity is **2018.3.x or greater**, if you don't satisfy that, use the [unitypackage](#2-install) method.<br>
2.2.1 - [if your Unity version is **2018.x.x**] Make sure that under `Edit -> Project Settings -> Player` the `Configuration -> Scripting Runtime Version` is set to **.NET 4.x Equivalent**.<br>
2.2.2 - Open `Packages/manifest.json` with your favourite editor and add the following in your `dependencies` (make sure to respect JSON commas):
```
{
 "dependencies": {
  ...
  "com.pusher.pusherwebsocketunity": "https://github.com/pusher/pusher-websocket-unity.git#2.3.0-beta+230104"
 }
}
```
2.2.3 - Now Unity should auto resolve dependencies and fetch the newly defined package.

### 3 IL2CPP Extra Steps
**NOTE:** You can ignore the following steps if using Mono

3.1 - Add the following to the `link.xml` file located at `/Assets`. If the file doesn’t exist, then create it.
```
<linker>
    <assembly fullname="PusherClient" preserve="all"/>
</linker>
```
3.2 - Don't use any methods in the PusherClient namespace that contain dynamic types. Using these methods will result in a runtime crash as IL2CPP doesn’t support dynamic types due to it's AOT compiler. An example of this is the `Channel.Bind(string, Action<dynamic>)` method, instead use the overload methods.

### 4 Add PusherManager and run the game
4.1 - Copy the sample [`PusherManager.cs`](BaseProject/Assets/PusherManager.cs) into your project's Assets folder and add your keys as values for `private const string APP_KEY` and `private const string APP_CLUSTER` obtained when you created the Pusher Channels app in the dashboard.<br>
4.2 - Create a new GameObject, by going on `GameObject -> Create Empty`. Drag the `PusherManager.cs` script onto the GameObject Inspector to set it as a script for the object.<br>
4.3 - Save and click *Play* to start the game in Unity.<br>
4.4 - Verify that `Connection state changed`, `Connected`, `Subscribed` is logged in the *Console* tab.<br>
4.5 - You can now customize the channel name (by default is `"my-channel"`) and events to bind to (by default is `"my-event"`) in the `PusherManager.cs` script.

## Update this package
### Update the version of .unitypackage
To update the version of the `.unitypackage` you can delete the `Assets/PusherWebsocketUnity` directory and repeat the [install steps](#2-install).

### Update the version of Unity Package Manager (UPM) package
To update the version of `com.pusher.pusherwebsocketunity` you just need to check the available versions in [releases](/../../releases) and change the package version in the `Packages/manifest.json`, like so:

From:
```json
"com.pusher.pusherwebsocketunity": "https://github.com/pusher/pusher-websocket-unity.git#0.0.0+000000"
```
To:
```json
"com.pusher.pusherwebsocketunity": "https://github.com/pusher/pusher-websocket-unity.git#2.3.0-beta+230104"
```

## Unity Platforms Support

### Supported Platforms:
The supported platforms should be the ones that can be targeted by Unity.
Thus far we tested this, and can confirm the library works, on:
- Windows
- MacOS
- Android
- iOS

### Unsupported Platforms:
- WebGL: due to incompatibility with Websockets (more [here](https://docs.unity3d.com/Manual/webgl-networking.html) under the _"No direct socket access"_ section)

<!--
### Update the Package
TODO

### Build
TODO
-->

## Credits
- Unity Technologies https://unity3d.com/company - for the Unity3d environment
- Patrick McCarthy (GlitchEnzo) https://github.com/GlitchEnzo - for [NuGetForUnity](https://github.com/GlitchEnzo/NuGetForUnity)
