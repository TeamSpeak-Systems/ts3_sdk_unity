TeamSpeak 3 Plugin for the Unity3D Game Engine
===============================================

About
-----

The Unity3D Plugin allows you to integrate the TeamSpeak 3 SDK client part into a Unity3D application and connect to a standalone
TeamSpeak 3 SDK Server.

The client SDK is a native C++ library. This package is a Native Code Plugin to create the bridge between the managed Unity C# 
code and the unmanaged TeamSpeak client library.

Setup
-----






You can call the functions directly using the static functions defined TeamSpeakInterface.cs.
This is not recommended since this means that you will have to manually release memory after calling some functions. If you still
want to do this, use the TeamSpeak SDK client manual to see where you need to release memory.

The TeamSpeakClient is a 'memory safe' wrapper for TeamSpeakInterface. All supported functions can be called trough this class.
By using this class you can easily use the callback functionality by editing the functions defined in TeamSpeakCallbacks.cs
Note that you first have to call TeamSpeakClient.StartClient or TeamSpeakClient.InitClientLib before you can use any other function.
The naming of the functions follow the names of the original SDK functions but without the ts3client_ prefix, and they start with a
uppercase character.

We recommend to use the auxiliary functions from the TeamSpeakClient class. In order to ensure platform independency, we recommend
the following:
- Use TeamSpeakClient.StartClient instead of connecting manually. This functions combines connecting to the server, and starting 
the sound devices for all supported platforms. Also, by using this function, the TeamSpeakClient will automatically store the
server connection handler.
- Use AddServerConnection instead of SpawnNewServerConnectionHandler. This function combines connecting to the server, and starting
the sound devices for all supported platforms. Also, by using this function, the TeamSpeakClient will automatically store the
server connection handler.
- You will see that there are a lot of functions where you can choose whether you want to specify the server connection handler id.
The server connection handler id is mandatory unless you have used StartClient and AddServerConnection. In this case the first
obtained connection handler will be used.


Notes for Android:
- When building for Android, you need to include the TeamSpeakAndroidEventHandler prefab into your scene. If this prefab is not
available, you will not receive any events.
- Custom password encryption is not supported on Android (Can't connect to a server using custom password encryption).

Notes for iOS:
- Unity 5: Only Scripting backend Mono2x is supported. You can find this option in Player Settings -> Other Settings.

Notes for OSX:
- Unity can just work with .bundle files. 

Notes that not all TeamSpeak callbacks are supported in Unity:
- onCustomPacketEncryptEvent
- onCustomPacketDecryptEvent

The following callbacks aren't supported on Android:
- onEditPlaybackVoiceDataEvent
- onEditPostProcessVoiceDataEvent
- onEditMixedPlaybackVoiceDataEvent
- onEditCapturedVoiceDataEvent
- onCustom3dRolloffCalculationClientEvent
- onCustom3dRolloffCalculationWaveEvent
- onCheckServerUniqueIdentifierEvent
- onClientPasswordEncrypt

Note that the TeamSpeak SDK clients will only work with the TeamSpeak SDK servers.
