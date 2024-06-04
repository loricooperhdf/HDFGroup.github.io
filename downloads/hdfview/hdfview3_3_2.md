---
title: HDFView 3.3.2
---

<img alt="HDFView Logo" align=right width=300 src="/assets/img/hdfview.png">

# HDFView 3.3.2

## Release Information

| Version | HDFView 3.3.2 |
| Release Date | 06/03/2024 |
| Additional Release Information | [Release Notes](https://github.com/HDFGroup/hdfview/blob/v3.3.2/docs/RELEASE.txt) |
| | [Release Announcement](https://www.hdfgroup.org/2024/05/release-of-hdfview-3-3-2-newsletter-203) | 
| | [Known Problems](#known-problems-in-this-release) |

## Documentation

| File | Type |
| ---- | ---- |
| [UsersGuide.tar.gz](https://hdf-wordpress-1.s3.amazonaws.com/wp-content/uploads/manual/HDFView/3.3.1/docs/UsersGuide.tar.gz) <br> [(sha256)](https://hdf-wordpress-1.s3.amazonaws.com/wp-content/uploads/manual/HDFView/3.3.1/docs/UsersGuide.tar.gz.sha256) | Documentation (HTML, Unix) | | 
| [UsersGuide.zip](https://hdf-wordpress-1.s3.amazonaws.com/wp-content/uploads/manual/HDFView/3.3.1/docs/UsersGuide.zip) <br> [(sha256)](https://hdf-wordpress-1.s3.amazonaws.com/wp-content/uploads/manual/HDFView/3.3.1/docs/UsersGuide.zip.sha256) | Documentation (HTML, Windows) | | |

## Download

HDFView 3.3.2 source and binaries are available [here](https://github.com/HDFGroup/hdfview/releases/tag/v3.3.2)

HDFView 3.3.2 was built and tested with HDF5-1.14.4-3, HDF 4.3.0, and openjdk 21. 

This release provides two ways to install the HDFView pre-built binary distribution for a platform:
* Using an application image. This method simply requires running the provided executable to obtain the software.
* Running an installer. This method runs an installer (eg .exe) that sets up file associations and menu items.

Once you have uncompressed the downloaded pre-built binary file, refer to the provided README file for details.

See Known Problems if you encounter any issues.

## Known Problems In This Release

* Workaround for issue with launching HDFView: A path issue which causes HDFView to fail to launch can be resolved by using the included batch script in the binary under the app folder.
* If installing HDFView with the installer method, please be aware that the installer does NOT overwrite "hardcoded" associations.  If there is a pre-existing user-defined file association, you must manually associate the extension with the HDFView application.

Please see the [Release Notes](https://github.com/HDFGroup/hdfview/blob/v3.3.2/docs/RELEASE.txt) for more information on known problems.
