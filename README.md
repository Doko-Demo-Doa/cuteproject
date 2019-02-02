# Cute Project

C++/Qt5 cross platform qmake subdirs example for desktop apps.

Implemented as one app/executable linked to multiple libs (modules).

[![Build Status](https://travis-ci.org/mxklb/cuteproject.svg?branch=master)](https://travis-ci.org/mxklb/cuteproject)
[![codecov](https://codecov.io/gh/mxklb/cuteproject/branch/master/graph/badge.svg)](https://codecov.io/gh/mxklb/cuteproject)
[![build status](https://gitlab.com/mxklb/cuteproject/badges/master/build.svg)](https://gitlab.com/mxklb/cuteproject/commits/master)
[![coverage report](https://gitlab.com/mxklb/cuteproject/badges/master/coverage.svg)](https://gitlab.com/mxklb/cuteproject/builds/artifacts/master/download?job=debug_tests)
[![Build status](https://ci.appveyor.com/api/projects/status/e4voihnpbh67ejm4/branch/master?svg=true)](https://ci.appveyor.com/project/mxklb/cuteproject/branch/master)
[![GitHub license](https://img.shields.io/badge/MIT-license-blue.svg)](https://raw.githubusercontent.com/mxklb/cuteproject/master/LICENSE)

This is a C++/Qt5 example with automated unit test execution ([catch](https://github.com/philsquared/Catch)). Tests are implemented in executables (subdirs) which get executed during compilation - compilation fails if one of these tests fail. This is the ideal precondition for test driven development. When using gcc, local [lcov](http://ltp.sourceforge.net/coverage/lcov.php) test coverage report generation is suported. Semantic versioning combined with continuous deployments is build on top while using free continuous integration services ([travis](https://travis-ci.org/), [gitlab](https://about.gitlab.com/product/continuous-integration/) & [appvoyer](https://www.appveyor.com/)) for open source development.

This project contains examples for:
- automated test execution with qmake (local)
- test coverage report creation with lcov (local)
- cross platform packaging (deb, AppImage, dmg & exe)
- cross platform CI builds (linux, macOS & windows)
- continuous artifact & release deployments (CI/CD)

Download latest development version here:
- [cuteproject-linux.x86_64.AppImage](https://gitlab.com/mxklb/cuteproject/builds/artifacts/master/download?job=appimage_latest)
- [cuteproject.ubuntu14.04_amd64.deb](https://gitlab.com/mxklb/cuteproject/builds/artifacts/master/download?job=debian_trusty_latest)
- [cuteproject.ubuntu16.04_amd64.deb](https://gitlab.com/mxklb/cuteproject/builds/artifacts/master/download?job=debian_xenial_latest)
- [cuteproject.macOS-latest.dmg](https://cdn.jsdelivr.net/gh/mxklb/cuteproject@osx-deploy/cuteproject.dmg)
- [cuteproject.windows_x86.zip](https://ci.appveyor.com/api/projects/mxklb/cuteproject/artifacts/cuteproject-windows_x86.zip?branch=master&job=Environment%3A+tbs_arch%3Dx64%2C+tbs_tools%3Dmsvc14%2C+tbs_static_runtime%3D0)

Note: This program does nothing famous. It just pops up a C++/Qt5 desktop UI which shall work cross platform. It's meant to be an example for a DevOps-driven desktop UI development. That's its only use case.

## Build Dependencies
To successfully build on debian based OS:

    sudo apt-get install qt5-default qt5-qmake gdb

To successfully build on macOS:

    brew update
    brew install qt5
    export PATH=$(brew --prefix)/opt/qt5/bin:$PATH

To successfully build on windows (install Qt & MSVC):

    call "C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\vcvarsall.bat"
    set PATH=%PATH%;C:\Qt\5.9\msvc2015\bin;C:\Qt\Tools\QtCreator\bin;

Note: Shall also work with other Qt or MSVC versions ..

## Build Instructions

    qmake
    make

Note: On windows use ```jom``` instead of ```make```

## Versioning
Cuteproject uses semantic versioning. Git tags on the master branch are used to mark specific versions. Git tags must have the form **1.2.3** (note: no prefix **v**). So github automatically creates releases. To automate artifacts versioning the ```pkgs/version.sh``` script utilizes ```git describe --long``` to create semantic version numbers.

## Packaging

This project contains scripts for automated packaging. All scripts are tested under linux, besides the *macOS.sh* script - it's implemented for Mac OS X only. All of these scripts can be called locally to produce the following build artifacts:

- ```pkgs/debian.sh``` creates a debian package
- ```pkgs/appimage.sh``` creates an .AppImage
- ```pkgs/macOS.sh``` creates a .dmg image

Note: Refer to the CI configurations to check for detailed packaging dependency information.

Windows packaging is actually only implemented within .appvoyer.yml!

## CI/CD Configuration
Development and testing is mainly focused on linux. Windows and Mac OS X are additionally used to verify builds and to make deployments. There are three different CI platforms configured ([travis](https://travis-ci.org/), [gitlab](https://about.gitlab.com/product/continuous-integration/) & [appvoyer](https://www.appveyor.com/)). The project is always build on linux, macOS and windows. Packages for these systems are always build and deployed.

The following operating systems get triggered continuously:

**Gitlab** (```git push``` triggered + weekly) :: Artifact = [.deb &  .AppImage]
- Ubuntu:devel (build & test)
- Ubuntu:rolling (build & test)
- Ubuntu:latest (build, test & deploy, ++[lcov](http://ltp.sourceforge.net/coverage/lcov.php))
- Ubuntu:trusty (build, test & deploy)
- Ubuntu:xenial (build, test & deploy)

**Travis** (```git push``` triggered) :: Artifact = Apple Disk Image [.dmg]
- Ubuntu:trusty (gcc -> build & test, ++[codecov](https://codecov.io/gh/mxklb/cuteproject))
- Ubuntu:trusty (clang -> build & test, ++[codecov](https://codecov.io/gh/mxklb/cuteproject))
- Mac OS X (gcc -> build, test & deploy)
- Mac OS X (clang -> build, test & deploy)

**AppVoyer** (```git push``` triggered) :: Artifact = Windows Executable [.exe]
- Windows x64 (Visual Studio -> build & deploy)
- Windows x64 (MinGW -> failing!)

Note: Refer to the configuration files for more detailed information.

## Development
Development takes place on [github](https://github.com/mxklb/cuteproject) while the repository is mirrored to [gitlab](https://gitlab.com/mxklb/cuteproject) for deployments ..

Pull requests are welcome - for contribution checkout [issues](https://github.com/mxklb/cuteproject/issues).
