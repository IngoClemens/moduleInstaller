# moduleInstaller
Installation script to install a module-based script or plug-in for Autodesk Maya.

It provides a standard way to install just about any module-based script or plug-in for Autodesk Maya without having the user create or edit module files manually nor copy files to the right locations. Modules are an easy way to distribute scripts or plug-ins but setting up paths the right way can often be misunderstood by the user. The installer takes care of all necessary steps.

## Installer scripts
All three installer files can be run with a double-click.

**install_macOS.command**
This is basically a regular shell script with a command extension to make it executable for macOS.

**install_linux64.desktop**
This is an executable linux desktop file which calls the _install_macOS.command script_. Therefore, when providing an installer for Linux both files (_install_linux64.desktop_ and _install_macOS.command_) must be present.

**install_win64.bat** is a regular Windows batch script.

## module.cfg
The installation of the module can be customized with the module.cfg file and should cover the most common setups. Used entries in this file override the default values within this script. The module.cfg file is not mandatory for the installer to work but mainly a way to customize without having to touch the installer in the first place. For more info see the header info and comments in the module.cfg file.

## Setup
After defining the specific paths for the module in the module.cfg file the installer works if the following requirements are met:

    - The module.cfg file must be present at the same folder level as the installer but is optional.
    - The module to be installed must be located within the **modules** folder which has to be present at the same folder level as the installer as well.
    - The license file with the name LICENSE also has to be present alongside the installer but is optional.

Folder structure:

    - LICENSE (optional)
    - module.cfg
    - installation script/s
    - modules/moduleName/moduleContent

See the folder structure in the sampleModule folder.

This structure has been chosen to make the locations of the module and folders obvious even when the installer is not being used. The topmost modules folder should hint that a module usually always goes to a folder named 'modules' within the Maya search paths. Within the 'modules' folder is the module folder which carries the name of the module. The installer takes the name of this folder to execute the installation. The module folder itself contains all the elements for the module: icons, plug-ins, scripts. The installer checks for the existance of the plug-ins folder which triggers how the module is defined. Usually, when plug-ins are present, it's necessary to setup version dependent module definitions. If the plug-ins folder is missing only a general module gets defined which can be loaded by all versions of Maya.

## Installation routine
    - Read the module.cgf file to determine how the module should be set up. If this file is missing the default values will be used (see module.cfg for more information).
    - Ask, if the installation should proceed.
    - Display the license agreement which is located in the same folder as the installer. If the license file is missing this part gets skipped. Declining the license ends the installation.
    - Give the option to do a simple or custom installation or create a module file only. The simple installation method removes existing files silently and installs at the default path. The custom installation allows for creating backups of existing files and lets the user choose the installation path and module file path. Creating a module file only is for advanced installations in custom studio environments. The generated module file is only meant as a template and aimed for users who know how to manually install modules.
    - Check for a previous installation of the module. For this only the default Maya module locations are taken into account. Additional custom locations are ignored. If the MAYA_APP_DIR variable is set this path will be included for the process as well.
        - If a previous module is found offer to delete the files.
        - If the files should not get deleted ask if a backup should be created. In this case the .mod file and the module folder are being moved to a new folder named after the module and the current time. This backup folder is located where the module has been found.
        - If creating a backup is declined the installation ends.
    - Display the path where the module will be installed.
    - Ask, if the provided path should be used.
    - If an alternative path should be used display a list of previously used install paths. Also give the option to enter a new path.
    - In case of a custom path let the user provide a new path. This path also gets stored in a file located in the users temp directory.
    - Display the path where the module file will be installed.
    - Ask, if the provided path should be used.
    - If an alternative path should be used display a list of previously used install paths. Also give the option to enter a new path.
    - In case of a custom path let the user provide a new path. This path also gets stored in a file located in the users temp directory.
    - Create the .mod file at the module path and copy the module files.
    - A log file gets created and saved in the same location as the installer.

## Changelog

**0.8.0 (2019-03-29)**

    - Fixed issues with paths containing spaces.

**0.7.0 (2019-03-26)**

    - When choosing to install in a new location display a list of previously used paths.
    - Use the first entry of the stored installation paths as the default install path.

**0.6.0 (2019-03-20)**

    - Initial open source release.
