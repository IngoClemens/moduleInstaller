# moduleInstaller
Installation script to install a module-based script or plug-in for Autodesk Maya.

It provides a standard way to install just about any module-based script or plug-in for Autodesk Maya without having the user create or edit module files manually nor copy files to the right locations. Modules are an easy way to distribute scripts or plug-ins but setting up paths the right way can often be misunderstood by the user. The installer takes care of all necessary steps.

If the module meets the basic requirements setting up the installer is mainly done by copying the installer files to the parent folder of the module.

## Description

See the [Wiki](https://github.com/IngoClemens/moduleInstaller/wiki) for full details.

## Changelog

**0.9.0 (2019-08-14)**

    - Fixed an issue with paths containing underscores on windows.

**0.8.0 (2019-03-29)**

    - Fixed issues with paths containing spaces.

**0.7.0 (2019-03-26)**

    - When choosing to install in a new location display a list of previously used paths.
    - Use the first entry of the stored installation paths as the default install path.

**0.6.0 (2019-03-20)**

    - Initial open source release.
