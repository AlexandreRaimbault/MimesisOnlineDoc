# Plugins Installation workflow

## Introduction

**Skyreal suite** provides a few plugins to customize your experiences, but we decided to create our owns to upgrade the experience, desktop or VR.

Our list of plugins can be found at : 

--- 

## Plugins export

Make sure to modify the Variables.json at the root of your project as it follows :

```json
// List only the plugins you wish to cook here
"ExtensionsPlugins": [
		"MyDummyPG"
	],

// Installer name can be changed for each plugin
	"InstallerName": "DummyTestInstall",
```

### Blueprint only plugins

If you are developping your plugin with the new SkrSample, you should have a script within the project to help you Build the plugin:
```
"C:\PathToProject\ressources\SkrExtensionScripts\scripts\Build-Repository.ps1"
```
When you run it, if there are no compiler errors, you will now have insisde the Output folder :
* An installer
* A cooked folder containing your plugin(s)

### C++ Plugins

As you may know, Skyreal doesn't like C++ Plugins  
You will need to package your project inside Unreal Engine to have a custom Skyreal version, that you can later use inside Deck, with the plugin working.

To do so you will need to :
1. Make sure to have SplashScreenLevel for GameDefaultMap in your Project Settings / Maps & Modes
2. No compiling errors when Packaging (Platforms/Windows/PackageProject)

If there are no compiler errors, you will now have insisde a Packaged folder :
* An .exe of Skyreal that you can try to launch and test with Skr Test map

We are currently working on a way to include multiples C++ plugins in a Custom Skyreal version.

---

## Plugins Installation

You can choose to install plugins locally for your Deck, or install them on the XRCenter

### Blueprint only plugins

Copy your Output directory to your XRCenter machine, and run the installer. You NEED to have the .skrapp file alongside the installer.  
Choose Marketplace install, and your plugin should be visible for every experience running the same version as you.

You can also try installing with the Legacy way inside the installer, it may be easier for standalone Deck and quick testing.

### C++ plugins

Once you have your packaged build you need to link it to every Deck installation where you want the C++ plugin running.  
To do so, set inside your "C:/ProgramData/Skr/1.21/deck/deck.json" file :  
```json
{
	"StandaloneXRCenterSettings": {
		"MarketplaceSettings": {
			"ScanDirectoryPath": "C:\\.skrpackages\\ScanDirectory",
			"PackageArchivesDirectoryPath": "%programdata%\\Skydea\\xrcenter\\packages",
			"ScanNewPackages": true
		}
	},
	"SkyRealExePath": "C:\\Users\\raimbaal\\Documents\\UE_Output\\test\\Windows\\Playground.exe"
}

```

--- 

## Plugins Maintenance

### Blueprint only plugins

We are currently working on a way to setup faster to update plugins on the marketplace.  
Currently, you need to remove the plugin from the list in "%programdata%\Skydea\xrcenter\packages" and relaunch the Installer exe

### C++ plugins

At the moment, we need to replace manually the packaged Skyreal version for each instance of Deck when we make modifications on our C++ plugin

---

## Known issues

* Issue where a map not created with Deck cannot be opened by Custom Skyreal with C++ plugins
* With Marketplace, known issue where a plugin is available only for UEEditor experience and NOT for Basic experience created with Deck
* With UEEditor experiences, when opened, can't create files in there because filepath created by Deck is too long.
* Deck will be replaced in Skyreal 1.22


