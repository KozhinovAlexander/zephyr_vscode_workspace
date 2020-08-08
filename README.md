# Zephyr Visual Studio Code Development Workspace Configuration
Zephyr Development VisualStudio Code Workspace configuration.

This simple repository provides Visual Studio Code (aka VSCode) necessary
configurations and scripts for [Zephyr](https://github.com/zephyrproject-rtos/zephyr) development:

* Configuration of VSCode workspace
* Build script
* Debugger script/launcher(currently only OpenOCD for STM32 series)
* OpenOCD STM32 config files

# Description of this repository

Here you can find the decription of this repository files. Depending on
new features development new description paragraphs can be added.

## 1. Checking out this repo
Run following command from `zephyrproject` folder
> git clone https://github.com/Nukersson/zephyr_vscode_workspace.git

**Note:** This repository must be placed in your `zephyrproject` folder!

## 2. Folder structure description

### 2.1. Visual Studio Code Workspace Configuration
The file `Zephyr.code-workspace` contains Visual Studio Code workspace
configuration and also TABs/SPACES and line margin configuration according to
[Zephyr's coding style Guide](https://docs.zephyrproject.org/latest/contribute/index.html#coding-guidelines)
