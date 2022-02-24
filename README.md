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
-  


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
