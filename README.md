
- [Zephyr Visual Studio Code Development Workspace Configuration](#zephyr-visual-studio-code-development-workspace-configuration)
	- [I. Usage description](#i-usage-description)
	- [1. Getting started](#1-getting-started)
	- [2. Workspace Configuration](#2-workspace-configuration)
	- [3. Workspace Tasks](#3-workspace-tasks)
		- [3.1 West Build Zephyr - Task](#31-west-build-zephyr---task)
		- [3.2 Set Zephyr Source - Task](#32-set-zephyr-source---task)
		- [3.3 Clean Build - Task](#33-clean-build---task)
		- [3.4 Stylcheck (commited only) - Task](#34-stylcheck-commited-only---task)
		- [3.5 GitLint (commited only) - Task](#35-gitlint-commited-only---task)
		- [3.6 Checkpatch (commited only) - Task](#36-checkpatch-commited-only---task)
		- [3.6 Generate Eclipse CDT4 - Task](#36-generate-eclipse-cdt4---task)
	- [4. Launching the project](#4-launching-the-project)
	- [5. Some Helpful Tricks](#5-some-helpful-tricks)
		- [5.1 Compiling wiht -O0](#51-compiling-wiht--o0)
		- [5.2 Cleaning untraked Git branches](#52-cleaning-untraked-git-branches)
	- [II. Folder Structure Description](#ii-folder-structure-description)
		- [2.1. Visual Studio Code Workspace Configuration](#21-visual-studio-code-workspace-configuration)

# Zephyr Visual Studio Code Development Workspace Configuration

Zephyr Development VisualStudio Code Workspace configuration.

This simple repository provides Visual Studio Code (aka VSCode) necessary
configurations and tasks for [Zephyr](https://github.com/zephyrproject-rtos/zephyr) development:

- Configuration of VSCode workspace
- Build, Clean, Debug Launch, Code Style Checks tasks
- OpenOCD STM32 config files
- stm32 SVD files needed for debugger

## I. Usage description

Here you can find the decription of this repository and it's usage. Depending on
new features development new description paragraphs can be added.

__NOTE:__ Currently only `Ubuntu Linux` with `zephyr-sdk-0.16.0` were tested!

You're also welcome to made changes on this repository.
Just fork it and provide PR with meaningfull changes you need.
I will bea ble to review it in couple of days.

## 1. Getting started

Follow this simple steps to simplify your Zephyr development in VSCode:

1. Follow Zephyr's latest [Getting Started Guide](https://docs.zephyrproject.org/latest/getting_started/index.html)
2. Switch to yout `zephyrproject` path from terminal:

```bash
cd <some_your_path>/zephyrproject
```

3. Clone this repository in your `zephyrproject`:

```bash
git clone https://github.com/KozhinovAlexander/zephyr_vscode_workspace
```

4. Open [Zephyr.code-workspace](https://github.com/KozhinovAlexander/zephyr_vscode_workspace/blob/master/Zephyr.code-workspace) as a workspace in VSCode: `File -> Open Workspace...`

__NOTE:__ last opened active workspace shall be closed
__NOTE:__ This repository must be placed in your `zephyrproject` folder!

## 2. Workspace Configuration

The [Zephyr.code-workspace](https://github.com/KozhinovAlexander/zephyr_vscode_workspace/blob/master/Zephyr.code-workspace)
contains all neccessary workspace configuration accepted by Zephyr project like:

- Folders to open (like `zephyrproject`)
- Minimal code styling settings (TABs/SPACES)
- Exclude paths (needed to reduce CPU usage while workspace is opened)

## 3. Workspace Tasks

There are some predefined tasks (see [.vscode/tasks.json](https://github.com/KozhinovAlexander/zephyr_vscode_workspace/tree/master/.vscode)) for simplifying of Build, Clean and Launch operations.

__NOTE:__ In VSCode a task can be run by typing `F1` and choosing the task you need.

### 3.1 West Build Zephyr - Task

__HowToRun:__ Press `F1` key and choose `Tasks: Run Build Task`, then choose `West Build Zephyr`

This task removes `zephyr/build` folder and compiles the project again.

In the file [.vscode/tasks.json](https://github.com/KozhinovAlexander/zephyr_vscode_workspace/tree/master/.vscode)
following environment variables are important:

- `BOARD_NAME` - defines name of the board to compile Zephyr appplication for
- `PRJ_NAME` - defines application/project name to compile

Change the above environment variables to the board and application name you need.

__NOTE:__ This task depend on `Clean Build` Task. You can remove it from
`dependsOn` list of this task to avoid removing of Zephyr's build folder each
time your application will be compiled!

### 3.2 Set Zephyr Source - Task

__HowToRun:__ Press `F1` key and choose `Tasks: Run Build Task`, then choose `Set Zephyr Source`

This task just runs following script:

```bash
./zephyr-env.sh
```

This is a service task and needed for `West Build Zephyr` Task.

__WARNING:__ Do NOT remove this task from the `dependsOn` list of `West Build Zephyr` Task!

### 3.3 Clean Build - Task

__HowToRun:__ Press `F1` key and choose `Tasks: Run Build Task`, then choose `Clean Build`

This task just runs following comand:

```bash
rm -rf build
```

The task is useful if you need refresh your build folder after switching between
branches for example. In this case `CMake` is not able to follow changes, which
are happening.

__NOTE:__ You may remove this task form `dependsOn` list of `West Build Zephyr` Task,
if you don't want wait long for compile and work whole the time on same project.

### 3.4 Stylcheck (commited only) - Task

__HowToRun:__ Press `F1` key and choose `Tasks: Run Task`, then choose `Stylcheck (commited only`

This task runs `GitLint (commited only)`and `Checkpatch (commited only)`tasks
one after other. Thus it checks code- and commits-style!

It is useful to run this task before you push your PR.

__NOTE:__ Uncommited changes will not be checked!

### 3.5 GitLint (commited only) - Task

__HowToRun:__ Press `F1` key and choose `Tasks: Run Task`, then choose `GitLint (commited only`

This task just runs following comand:

```bash
gitlint
```

The task is used for commits-style checking

__NOTE:__ Uncommited changes will not be checked!

### 3.6 Checkpatch (commited only) - Task

__HowToRun:__ Press `F1` key and choose `Tasks: Run Task`, then choose `Checkpatch (commited only`

This task just runs following comand:

```bash
${ZEPHYR_BASE}/scripts/checkpatch.pl -g HEAD-10
```

The task is used for code-style checking. It checks last 10 commits (see `HEAD-10`)
from `HEAD`. You may change `HEAD-N` to check last `N` commits (see [.vscode/tasks.json](https://github.com/KozhinovAlexander/zephyr_vscode_workspace/tree/master/.vscode)).

__NOTE:__ Uncommited changes will not be checked!

### 3.6 Generate Eclipse CDT4 - Task

__HowToRun:__ Press `F1` key and choose `Tasks: Run Build Task`, then choose `Generate Eclipse CDT4(commited only`

This task creates `Eclipse CDT4` files to import the project into Eclipse.

## 4. Launching the project

To launch the project you need [Cortex-Debug](https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug)
extension for Visual Studio Code. Please install it and follow it's installation guide.

It can be also helpfull to follow [OpenOCD for Zephyr](https://github.com/zephyrproject-rtos/openocd) installation description,
especially if you're using `ST-LINK V3` debug adapter.

After installing `Cortex-Debug` and `OpenOCD` on your system, the debug buttun
should appear in your VSCode GUI.

The [.vscode/launch.json](https://github.com/KozhinovAlexander/zephyr_vscode_workspace/blob/master/.vscode/launch.json)
describes launch configuration for `Cortex-Debug`. In this file you may choose following settings:

- Current board name
- SVD file name
- Debug interface
- Debugger

## 5. Some Helpful Tricks

### 5.1 Compiling wiht -O0

Add following line to Zephyr's main CMakeLists.txt:

```cmake
set_source_file_properties(<path_to>/<some_source>.c PROPERTIES COMPILE_OPTIONS  "-O0")
```

to compile `<path-to>/<some_source>.c` wile with -O0.

### 5.2 Cleaning untraked Git branches

Aftersiwtching between different remote repositiries you may want delete local
unracked branches. You can do it by typing following command in your terminal,
while location in your working git repository:
> git fetch -p && git branch --merged | grep -v '*' | grep -v 'master' | xargs git branch -d

__Explanation:__

- `git fetch -p` - will prune all branches no longer existing on remote
- `git branch -vv` - will print local branches and pruned branch will be tagged with gone
- `grep ': gone]'` - selects only branch that are gone
- `awk '{print $1}'` - filter the output to display only the name of the branches
- `xargs git branch -D` - will loop over all lines (branches) and force remove this branch

taken from [this source](https://stackoverflow.com/questions/7726949/remove-tracking-branches-no-longer-on-remote)

## II. Folder Structure Description

### 2.1. Visual Studio Code Workspace Configuration

The file `Zephyr.code-workspace` contains Visual Studio Code workspace
configuration and also TABs/SPACES and line margin configuration according to
[Zephyr's coding style Guide](https://docs.zephyrproject.org/latest/contribute/index.html#coding-guidelines)
