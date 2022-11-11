# Unity project recommendation guideline

Rewrite of the juegostudio [publication](https://www.juegostudio.com/blog/7-ways-to-keep-unity-project-organized-unity3d-best-practices) and [this](https://github.com/stillwwater/UnityStyleGuide) naming convention.

# Table of contents
- Guideline
    - [Introduction](#introduction)
    - [Folder structure](#directory-or-folder-structure)
    - [Scene hierarchy](#managing-the-scene-hierarchy-structure)
    - [Version control systems](#get-familiar-with-version-control-systems-or-vcs)
    - [Prefabs](#use-prefabs-more-frequently)
    - [Editor scripts](#get-familiar-with-editor-scripts)
    - [Defensive programming](#learn-and-implement-defensive-programming)
    - [Editor cheats](#try-in-game-andor-in-editor-cheats)
-  Naming Convension
    - [Asset Naming](#asset-naming)
    - [Folders](#folders)
    - [Debug folders](#debug-folders)
    - [Source Code](#source-code)
    - [Non code assets](#non-code-assets)
    - [Scripts](#scripts)
    - [Models](#models)
    - [Workflow](#workflow)
        - [Models](#models-1)
        - [Textures](#textures)
        - [Texture suffixes](#texture-suffixes)
        - [RGB Masks](#rgb-masks)
        - [Configuration files](#configuration-files)
        - [Localization](#localization)
        - [Audio](#audio)

## Introduction

App development is a cumbersome process. Everything should be well organized, otherwise introducing changes can be a hard job. The same goes for Unity3D app development. As developers move on with the development process, lines of code increases. And this expands the final magnitude of the project.

## Directory or folder structure

The directory or folder structure is quite important for a well-organized Unity3D project. In Unity, you can place or name files according to your needs. And this freedom is what creates the entire mess. Here’s a basic template showing how an organized directory should look like: 
```
└───Assets
    ├───3rd-Party
    ├───Animations
    ├───Audio
    │   ├───Music
    │   └───SFX
    ├───Materials
    ├───Models
    ├───Plugins
    ├───Prefabs
    ├───Resources
    ├───Sandbox
    │   └───Username
    ├───Scenes
    │   ├───Levels
    │   └───Other
    ├───Scripts
    │   └───Editor
    └───Textures
```
#### Omit spaces in file names
Make sure that you never use spaces in folder or file names. It’s because Unity3D never processes paths with spaces on its own. Instead, write a command to do so.
#### Avoid storing assets in the root directory
The root directory is not where you can dump anything. So, use subdirectories for storing assets instead of root directories.
#### Naming conventions
If you use camel case while naming files, continue to do that. The motive here is to be consistent with the file names.
#### Use the ‘Sandbox’ directory for experiments
If you’re making some changes you aren’t sure about, make it in Sandbox. In Sandbox the structure doesn’t matter. You can create a personal Sandbox subdirectory like ‘Sandbox/your name’. And once you’re sure about the changes, you can move the data to the real project.

## Managing the Scene Hierarchy Structure
Similar to the project hierarchy, there’s a scene hierarchy you need to follow. Here’s a template of a well-organized scene hierarchy structure
```
───Scene
   ├───World
   ├───Lights
   ├───Cameras
   ├───_Dynamic
   ├───GUI
   └───Scene_Manager
```
#### Put objects instantiated during runtime into the 'Dynamic' folder
It’ll help you easily navigate the files.
#### Use empty game objects as scene folders
You need to organize the scenes carefully. It is done in order for you to find the objects when you’re looking for them.
#### Make sure that your project can run from every scene
When every scene will become runnable, you won’t have to spend much time testing. It’ll be more convenient to test the application

## Get familiar with version control systems or VCS
You must learn version control software such as GIT, SourceTree or Subversion. Such version control systems are much more than you think. It is not only used to create a backup or sync, but you can also use it to stash the unwanted changes.

Say, for example, you’re using GIT and working on the master branch. And you’re unsure of what some code might do to your code. Or you simply want to test that code later on. In such cases, you can stash the unwanted block of code.

Now, you can work on that code whenever you want without disturbing the master branch. Amazing, right?

You also don’t need to comment on large chunks of code you don’t want. If you use a VCS or version control system, you can access the previous version where the code was intact. This way you can avoid chunks of commented code. It’ll make your code look clean.

## Use prefabs more frequently
If you can, use prefabs for everything. Using prefabs, you can easily share pre-configured project hierarchies. Prefab is a fully configured reusable object which can be shared between scenes and projects. It is quite helpful when you want to add functionality to 100 scenes at a time.

Let’s say you need to add a camera effect to 200 levels. Now, if you have a camera prefab, it’s easy. You need to add a camera effect to the camera prefab, and you’re done. It’ll provide the functionality to each level regardless of the count.

## Get familiar with editor scripts

Unity is a pretty extensive game engine. And to leverage it, you need to learn editor scripts. Editor scripts are commands or a piece of code to alter the functionality in a Unity editor. You can create scripts for:

* Downloading files directly from the google drive folder
* Compressing all the files in a folder and storing them at a secure place
* Arranging all the objects in a scene

If you need more insights about creating an editor script, please refer [here](https://learn.unity.com/tutorial/editor-scripting#5c7f8528edbc2a002053b5f6).

## Learn and implement defensive programming

Defensive programming, in simple terms, is a way of coding defensively. Using defensive programming, you ensure that your software works under unforeseen circumstances. It’s usually followed when you deal with something that can be misused.

Whenever you write the base class (MonoBehaviours) in Unity make sure that

* You set all the references
* There’s no required component missing 
* Use ExecuteInEditMode and #if UNITY_EDITOR for performing checks before you play or run a scene.

## Try in-game and/or in-editor cheats

Now, this is something interesting. Once you learn how to write editor scripts, try adding in-editor cheats. 
You can add the functionality of unlocking secret levels to the user or something similar. You can write cheats that allow you to

* Add or reduce time/Lives or coins 
* Unlock secret characters or levels 
* Give immortality to your character 
* Do anything that helps you with testing.

# Asset naming

First of all, no\ spaces\ on file or directory names.

## Folders

`PascalCase`

Prefer a deep folder structure over having long asset names.

Directory names should be as concise as possible, prefer one or two words. If a directory name is too long, it probably makes sense to split it into sub directories.

Try to have only one file type per folder. Use `Textures/Trees`, `Models/Trees` and not `Trees/Textures`, `Trees/Models`. That way its easy to set up root directories for the different software involved, for example, Substance Painter would always be set to save to the Textures directory.

If your project contains multiple environments or art sets, use the asset type for the parent directory: `Trees/Jungle`, `Trees/City` not `Jungle/Trees`, `City/Trees`. Since it makes it easier to compare similar assets from different art sets to ensure continuity across art sets.

### Debug Folders

`[PascalCase]`

This signifies that the folder only contains assets that are not ready for production. For example, having an `[Assets]` and `Assets` folder.

## Source Code

Use the naming convention of the programming language. For C# and shader files use `PascalCase`, as per C# convention.

## Non-Code Assets

Use `tree_small` not `small_tree`. While the latter sound better in English, it is much more effective to group all tree objects together instead of all small objects.

`camelCase` where necessary. Use `weapon_miniGun` instead of `weapon_gun_mini`. Avoid this if possible, for example, `vehicles_fighterJet` should be `vehicles_jet_fighter` if you plan to have multiple types of jets.

Prefer using descriptive suffixes instead of iterative: `vehicle_truck_damaged` not `vehicle_truck_01`. If using numbers as a suffix, always use 2 digits. And **do not** use it as a versioning system! Use `git` or something similar.

### Persistent/Important GameObjects

`_snake_case`

Use a leading underscore to make object instances that are not specific to the current scene stand out.

### Debug Objects

`[SNAKE_CASE]`

Enclose objects that are only being used for debugging/testing and are not part of the release with brackets.

## Scripts

Use namespaces that match your directory structure.

A Framework directory is great for having code that can be reused across projects.

The Scripts folder varies depending on the project, however, `Environment`, `Framework`, `Tools` and `UI` should be consistent  across projects.

```
Scripts
+---Environment
+---Framework
+---NPC
+---Player
+---Tools
\---UI
```

## Models

Separate files from the modelling program and ready to use, exported models.

```
Models
+---Blend
\---FBX
```

# Workflow

## Models

File extension: `FBX`

Even though Unity supports Blender files by default, it is better to keep what is being worked on and what is a complete, exported model separate. This is also a must when using other software, such as Substance for texturing.

Use `Y up`, `-Z forward` and `uniform scale` when exporting.

## Textures

File extension: `PNG`, `TIFF` or `HDR`

Choose either a `Specularity/Glossiness` or `Roughness/Metallic` workflow. This depends on the software being used and what your artists are more comfortable with. Specularity maps have the advantage of being having the possibility to be RGB maps instead of grayscale (useful for tinted metals), apart from that there is little difference between the result from either workflow.

### Texture Suffixes
#### All of the textures must have a `Tex_` prefix.


Suffix | Texture
:------|:-----------------
`_D`  | Albedo/Diffuse
`_SP`  | Specular
`_R`   | Roughness
`_MT`  | Metallic
`_GL`  | Glossiness
`_N`   | Normal
`_H`   | Height
`_DP`  | Displacement
`_E`  | Emission
`_AO`  | Ambient Occlusion
`_M`   | Mask

### RGB Masks

It is good practice to use a single texture to combine black and white masks in a single texture split by each RGB channel. Using this, most textures should have:

```
texture_AL.png  # Albedo
texture_N.png   # Normal Map
texture_M.png   # Mask
```

Channel | Spec/Gloss        | Rough/Metal
:-------|:------------------|:-----------
R       | Specularity       | Roughness
G       | Glossiness        | Metallic
B       | Ambient Occlusion | Ambient Occlusion

#### The blue channel can vary depending on the type of material:

 - For character materials use the `B` channel for *subsurface opacity/strength*
 - For anisotropic materials use the `B` channel for the *anisotropic direction map*

## Configuration Files

File extension: `JSON`

Fast and easy to parse, clean and easy to tweak.

`XML`, `INI`, and `YAML` are also good alternatives, pick one and be consistent.

Use binary file formats for files that should not be changed by the player. For multiplayer games store configuration data on a secure server.

## Localization

File extension: `CSV`

Widely used by localization software, makes it trivial to edit strings using spreadsheets.

## Audio

File extension: `WAV` while mixing, `OGG` in game.

Preload small sound clips to memory, load on the fly for longer music and less frequent ambient noise files.

# Be Consistent

> The point of having style guidelines is to have a common vocabulary of coding so people can concentrate on what you're saying rather than on how you're saying it. We present global style rules here so people know the vocabulary, but local style is also important. If code you add to a file looks drastically different from the existing code around it, it throws readers out of their rhythm when they go to read it. Avoid this.

-- [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)

---
