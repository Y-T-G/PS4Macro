# PS4 Macro

[![Twitter](https://img.shields.io/twitter/url/https/twitter.com/fold_left.svg?style=social&label=Follow%20Me)](https://twitter.com/itskomefai)
[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](http://paypal.me/Komefai)

Automation utility for PS4 Remote Play written in C# using [PS4RemotePlayInterceptor](https://github.com/komefai/PS4RemotePlayInterceptor).

#### Screenshot

![Screenshot](https://raw.githubusercontent.com/komefai/PS4Macro/master/_resources/Screenshot_0_4_0.png)

## Usage

**Download latest version [here](https://github.com/komefai/PS4Macro/releases)!**

To record, click on `RECORD` button (Ctrl+R) to arm recording then press `PLAY` to start recording controls. The red number on the bottom right indicates the number of frames recorded. You can stop recording by clicking on `RECORD` button (Ctrl+R) again. The macro will then play the controls in a loop.

See [this video](https://youtu.be/txI9AOEAk58) for basic usage / making of.

## Settings

You can create `settings.xml` and place it with the executable to override default settings.

| Setting | Description | Default
| --- | --- | --- |
| AutoInject | Automatically poll for PS4 Remote Play and inject whenever possible | false |
| EmulateController | Run with controller emulation (use without a controller) | false |
| ShowConsole | Open debugging console on launch | false |
| StartupFile | Absolute or relative path to file to load on launch (can be xml or dll) | null |

##### Example settings.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings>
  <AutoInject>true</AutoInject>
  <EmulateController>true</EmulateController>
  <ShowConsole>true</ShowConsole>
  <StartupFile>MyMacro.xml</StartupFile>
</Settings>
```

## Scripting

C# scripting support has been introduced in version 0.3.0 and later. This allows us to create custom behaviors beyond repeating macros with an easy-to-use API. The API also includes wrapped convenience functions such as pressing buttons, timing, and taking a screenshot from PS4 Remote Play. 

See the [scripting video tutorial](https://youtu.be/daCb97rbimA) to get started or see [the wiki](https://github.com/komefai/PS4Macro/wiki) for full documentation, examples, and other information.

NOTE: The script have to include a reference to `PS4MacroAPI.dll` to interface with PS4Macro. At the moment the scripts has to be compiled into a DLL file to be able to open with PS4 Macro.

##### Basic Example Script

This example script will press DPad up and wait one second, follow by pressing square. The loop repeats every 800ms.

```csharp
using PS4MacroAPI;

public class Script : ScriptBase
{
    /* Constructor */
    public Script()
    {
        Config.Name = "Example Script";
        Config.LoopDelay = 800;
    }

    // Called when the user pressed play
    public override void Start()
    {
        base.Start();
    }

    // Called every interval set by LoopDelay
    public override void Update()
    {
        Press(new DualShockState() { DPad_Up = true });
        Sleep(1000);
        Press(new DualShockState() { Square = true });
    }
}
```

#### List of Scripts

- [Keyboard Remapping Utility](https://github.com/komefai/PS4Macro.Remote)
- [Marvel Heroes Omega Bot](https://github.com/komefai/PS4Macro.MarvelHeroesOmega)

## Troubleshoot

##### Macro not playing/recording

=> Disable AutoInject in settings.xml since some machines does not support AutoInject.

##### Visual Studio Build Error

=> Reinstall NuGet Package.

```
Update-Package –reinstall PS4RemotePlayInterceptor
```

## To-Do List

- ~~Save/Load~~
- ~~Keyboard Shortcuts~~
- ~~Status Indicators~~
- ~~Scripting~~
- ~~Use without DualShock controller~~
- Improve Scripting API Docs
- Playback Timeline UI
- Macro editor tool
- ...

## Resources

- [Tutorial Video](https://youtu.be/txI9AOEAk58)
- [Scripting Tutorial Video](https://youtu.be/daCb97rbimA)
- [Prototype Demo Video](https://youtu.be/QjTZsPR-BcI)

## Credits

- [EasyHook](https://easyhook.github.io/)
- [Jays2Kings/DS4Windows](https://github.com/Jays2Kings/DS4Windows)
- [jforshee/ImageHashing](https://github.com/jforshee/ImageHashing)
