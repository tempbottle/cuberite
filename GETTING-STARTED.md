Hello! Thanks for wanting to work on this project :smile:, and I hope that this file will help you somewhat in getting all set up and running. I'll go through the basics of getting the projet environment set up, the code organization and style, and general development practices. I'll also show you some good issues to start off working on to get yourself familiarised with the code.

Minecraft Basics
----------------

If you don't play Minecraft or don't have a great knowledge of the basic systems, you should get to know them. The [Minecraft Wiki](http://minecraft.gamepedia.com/Minecraft_Wiki) is quite useful for this task, although some youtubers are also fairly good at teaching the basics and just playing is quite good too. It is possible to contribute without knowing minecraft in detail though.

I'd say that the important topics are:

* Differnt types of blocks and how they act.
* Mobs, what they do and how.
* Redstone, pistons, and automation.
* Farming.
* Fighting, health and the hunger system.

Useful Resources
----------------

 * [Minecraft Wiki](http://minecraft.gamepedia.com/Minecraft_Wiki)
 * [Minecraft Protocol Wiki](http://wiki.vg)
 * [Lua API Documentation](http://mc-server.xoft.cz/LuaAPI)
 * [VS2013 Community Edition Download](https://www.visualstudio.com/products/visual-studio-community-vs)

Setting up a Dev Environment
============================

Requirements
------------

**Linux/BSD/Solaris/OSX:**

You'll need the basic C++ build tools:

 * gcc (or clang or another C compiler)
 * g++ (or clang++ or another C++ compiler)
 * make
 
You'll also need CMake to generate the makefile to build from.

**Windows:**

If you use Windows, your best bet is the MSVC2013 (available as a free download in the Community edition from MS), solution files for which can be generated with cmake. You'll also need cmake to generate the project files.

Setting up the Repo
-------------------

Next, you'll need to set up the repo. You should make a fork and work on that, then create a Pull Request so that we can review and merge your code. After you've "earned" an honorable status, we'll give you write access to the repository, so that you can work on branches in the main repo here (still use PRs though, they're great tools for review and discussion).

Once you've cloned, you need to pull down the submodules:

    git submodule init
    git submodule update

After that they should come down automatically when you pull but it's not bad to refresh every once in a while.

Repo Arrangement
---------------------------

The Cuberite repo has recently been rearranged for better code separation and other things, but basically it's split into a few areas:

 * `src`  
   This holds all of the Cuberite source code, and is where most development takes place.  
   It's split into logical areas for blocks, the protocol handling and other things.
 * `lib`  
   This holds all the 3rd party libraries for Cuberite. You basically don't need to touch these, and we're thinking of switching them into submodules soon.
 * `MCServer`  
   This folder isn't greatly named, but it contains the default plugins and environment to actually run the server. You'll find the executable (named `MCServer`) here and in the `plugins` subdir the default plugins. The config files are also stored here. Config files with `.example.ini` on the end are generated by the server or source control and should be left alone, instead you should copy them to a file without the `example` in the name which will be prioritised over the generated ones.

Code Styles
------------------

Mainly follow the code styles in [CONTRIBUTING.md](https://github.com/cuberite/cuberite/blob/master/CONTRIBUTING.md), which is definitely an important read.

Note that there is a script file, $/src/CheckBasicStyle.lua, that can check some common violations of the coding style. You should run this file to check your code regularly. This script is run during the integration builds and if it fails, the build will fail. Note that you need Lua installed in order to run this script.


How to Build
------------------

**Linux/BSD/Solaris/OSX:**

Follow the instructions in [COMPILING.md](https://github.com/cuberite/cuberite/blob/master/COMPILING.md). You probably want to build in debug mode (when you're developing) for console alerts and debugging capability, even though it's much slower for everyday use.

Basically, the process is:

    cmake . -DCMAKE_BUILD_TYPE=DEBUG && make

**Windows:**

You need to first generate a solution file by executing `cmake .` on the commandline at the top-level folder of the repository, then just open the solution file in MSVC and build. Note that the first time after generating the solution, you will need to do extra setup in order to be able to fully debug in MSVC:
- Set the startup project to Cuberite: right-click the MCServer project in the Solution Explorer and choose "Set as Startup Project".
- Set the debugging folder: right-click the MCServer project in the Solution Explorer, choose "Properties". In the dialog, browse to "Configuration Properties" -> "Debugging" and set "Working Directory" to "../MCServer".

How to Run
----------

The server can be run (on *nix) by a simple `./MCServer` in the `MCServer` directory. On first run it will generate the world and start a server on the default port (configurable in `settings.ini`) so you can connect in minecraft via `localhost`. Note that if you build a debug version, the executable will be names `MCServer_debug` instead

Where to Get Started
-------------------------------

There are a few fairly easy issues for you to get started with, as well as some more difficult but interesting ones.

**Easy**:

 * #140
 * #493
 * #577
 * #381
 * #752
 * Clean up some of the compiler warnings. (Check [Travis CI](http://travis-ci.org/cuberite/cuberite) for a list of them.) With clang, there are over 10000 lines of warnings to clean up.

**More Difficult**:

 * #133
 * #134
 * #215

You may also want to write some plugins. They are written in lua, with excellent API documentation available via [APIDump](http://api-docs.cuberite.org). The [Core](https://github.com/mc-server/Core) plugin should also help quite a bit here.

Special Things
---------------------
 * Make yourself familiar with the community. Visit the forums: http://forum.mc-server.org
 * Ask questions as much as you like, we're here to help :smiley: 
