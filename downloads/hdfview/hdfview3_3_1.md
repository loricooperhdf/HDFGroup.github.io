# HDFView 3.3.1

## Release Information

| Version | HDFView 3.3.1 |
| Release Date | 07/07/2023 |
| Additional Release Information | [Release Notes](https://github.com/HDFGroup/hdf5/blob/hdf5_1_14_3/release_docs/RELEASE.txt) |
| | [Release Announcement](https://www.hdfgroup.org/2023/04/release-of-hdfview-3-3-0-newsletter-193/) | 
| | Documentation | 
| | Known Problems |

## Files 

HDFView 3.3.1 was built and tested with HDF5-1.14.0, HDF 4.2.16-2, and openjdk 19. 

This release provides two ways to install the HDFView pre-built binary distribution for a platform:
* Using an application image. This method simply requires running the provided executable to obtain the software.
* Running an installer. This method runs an installer (eg .exe) that sets up file associations and menu items.

Once you have uncompressed the downloaded pre-built binary file, refer to the provided README file for details.

See Known Problems if you encounter any issues.

| File | Type | Install Instructions |
| ---- | ---- | ---- | 
| hdfview-3.3.1.tar.gz <br> (sha256) | Source Code (Unix) | Build Instructions | 
| hdfview-3.3.1.zip <br> (sha256)	| Source Code	(Windows) | Build Instructions | 
| HDFView User's Guide <br> (sha256) | Documentation (PDF) | | 
| UsersGuide.tar.gz <br> (sha256) | Documentation (HTML, Unix) | | 
| UsersGuide.zip <br> (sha256) | Documentation (HTML, Windows) | | |
| Pre-built binaries | Unix and Windows | All pre-built HDFView binary distributions provided

## Known Problems In This Release

* Workaround for issue with launching HDFView: A path issue which causes HDFView to fail to launch can be resolved by using the included batch script in the binary under the app folder.
* If installing HDFView with the installer method, please be aware that the installer does NOT overwrite "hardcoded" associations.  If there is a pre-existing user-defined file association, you must manually associate the extension with the HDFView application.

Please see the Release notes for more information on known problems.
