Source Files
============

For convenience, the sudo source tarball of version 1.7.10p7 which is used
to build the updated OS X version has been included in this directory.

Information on how to obtain it (and other source tarballs related to the OS X
version of sudo) directly follows.

# Version used in fully updated OS X 10.4.11 & 10.5.8
http://opensource.apple.com/tarballs/sudo/sudo-28.tar.gz
SHA-256: 415be55dc13c8840e4084bfa083da11d0516ea49b54923aa6897e377bade21a4
NOTE: Applying all the patches in the patches subdirectory to the 1.6.8p12
sources does indeed produce the contents of the sudo subdirectory.

# Version used in fully updated OS X 10.6.8
http://opensource.apple.com/tarballs/sudo/sudo-46.tar.gz
SHA-256: 968fae7e77162509626ef43f454fdedf13a2916c20cab31d1725339b50560162
NOTE: There is no included source tarball nor any distinct patches. :(
The original version number, however, is found in src/version.h (1.7.0).

# Version used in OS X 10.8.4
http://opensource.apple.com/tarballs/sudo/sudo-67.tar.gz
SHA-256: 36fa6d20a6b50f509b38e1d4484631972eaebc272bce84f47b1cc6b277f4be85
NOTE: There is no included source tarball nor any distinct patches. :(
The original version number, however, is found in src/config.h (1.7.4p6).
NOTE: Does not include sudo -k fix (fix is in 10.8.5 version)

# The original 1.6.8p12 sources for OS X 10.4.x/10.5.x version
http://www.sudo.ws/sudo/dist/OLD/sudo-1.6.8.tar.gz
SHA-256: 56eb8e12247a6932500099946bc18e412c1e0b071e0486c5a53f7f9e9642c70c
http://www.sudo.ws/sudo/dist/OLD/sudo-1.6.8p12.patch.gz
SHA-256: cd1ff07acd6708a66c2f07137765cca74dd3a9fd32f75944d6021c6ec4d789ab

# Apple's 1.6.8p12 source tarball
http://opensource.apple.com/source/sudo/sudo-28/sudo-1.6.8p12.tar.gz
SHA-256: 56f7d86032538a4a98d90af3742903a09ba16d6db82b593e4a47605f87fa581a
NOTE: Contents are the same as 1.6.8 with 1.6.8p12 applied except that the
three *.cat files are also updated in this tarball which 1.6.8p12.patch does
not actually do -- that should not matter as those can be rebuilt from the
man sources which are correctly updated by the 1.6.8p12.patch file.

# The original 1.7.0 sources for OS X 10.6.x version
http://www.sudo.ws/sudo/dist/OLD/sudo-1.7.0.tar.gz
SHA-256: 5f7de94287f39c8b3b8d86aed147967e9286f45740412004233858b637391978

# The original 1.7.4p6 sources for the OS X 10.8.4 version
http://www.sudo.ws/sudo/dist/sudo-1.7.4p6.tar.gz
SHA-256: 20091ef71018698c674c779f4b57178b2ecb4275fa34909b06219d2688ad14d5

# The 1.7.10p7 sources that include the sudo -k fix
http://www.sudo.ws/sudo/dist/sudo-1.7.10p7.tar.gz
SHA-256: 387a8fd136f9550d5d24c34d1856a9a6d26ed2771ad32df712852c73461c86b5

# The SHA256 checksums for www.sudo.ws/sudo/dist files
http://www.sudo.ws/sudo/dist/SHA256
http://www.sudo.ws/sudo/dist/OLD/SHA256
