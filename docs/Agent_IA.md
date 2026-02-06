# Agent_IA Plugin

## Overview

**Agent_IA** is an AI Agent plugin from the **Mimesis** project.  
It is designed to run **independently**, without requiring other Mimesis plugins.

The plugin integrates directly into the **Skyreal suite** and can be accessed inside Skyreal VR:

- from the **Right Menu** (With that little :simple-githubcopilot:)

- or through a **Resizable UI** (By pressing L on your Keyboard)

Agent_IA communicates with a **custom Ollama Agent**, specialized in **Data Science** tasks, and is working with a custom websocket server (Currently running remotely on our calcul station), and is fully **compatible with other Mimesis Plugins**.

If you want to know more about our custom LLM and our websocket server, you can read [this](Conversational_Generative_AI.md) page.

---

## Installation

You can install the plugin using one of the following methods.


### Local Copy Installation

1. Clone the repository **`Mimesis_AI_Agent`** locally  
   (via `.zip` download or Git URL).

2. Copy the plugin folder into your project:
   <YourProject>/
   └─ Plugins/
      └─ Mimesis_AI_Agent/  
    If the Plugins folder does not exist, create it at the root of your project.

3. Launch the project. If Unreal Engine requires recompilation, follow the steps below.

### Recompilation (if required)

If your project has **no `.sln` file**, C++ support is not enabled yet:

1. Right-click on the `.uproject`
2. Select **More options**
3. Click **Generate Visual Studio project files**

Then:

1. Open **Visual Studio** as **Administrator**
2. Open the generated `.sln` file
3. Right-click on the **Solution**
4. Select **Generate**

If no build errors occur, the plugin is ready to use.

---

### Submodule Installation

1. Open a terminal (PowerShell or equivalent)
2. Navigate to the root of your project
3. Go to the `Plugins` folder (create it if necessary)
4. Add the plugin as a Git submodule:

```bash
git submodule add https://gricad-gitlab.univ-grenoble-alpes.fr/mimesis/ai_agent_plugin
```

5. Commit the changes, including the .gitmodules file
6. Launch the project. 
If Unreal Engine requires recompilation, follow the same recompilation steps described above.

### Submodule Update

To update this plugin (and any other submodules), run the following command from the root of your project:
```bash
git submodule update --remote
```

For more information about Git submodules, refer to the official Git documentation.


## Package the Plugin

As you may know, Skyreal doesn't like C++ Plugins, and this plugins uses some for the websocket service.
You will need to package your project inside Unreal Engine to have a custom Skyreal version, that you can later use inside Deck, with the plugin working.

To do so you will need to :
1. Make sure to have SplashScreenLevel for GameDefaultMap in your Project Settings / Maps & Modes
2. No compiling errors when Packaging (Platforms/Windows/PackageProject)
3. Set inside your deck.json file :
```
"SkyRealExePath": "C:\\Users\\YourPathToThePackagedApp\\Windows\\Playground.exe"
```

We are currently working on a way to include multiples C++ plugins in a Custom Skyreal version.
