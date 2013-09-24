================
SUDO OS X UPDATE
================

-------------
What is this?
-------------

This project brings together the OS X specific patches for sudo together with
the official sudo 1.7.10p7 release to provide a fix for the CVE-2013-1775 [1]
vulnerability (details in [2]) to Mac OS X versions prior to 10.7.5/10.8.5
specifically versions 10.4.11, 10.5.8 and 10.6.8.

----------
Background
----------

Apple has included a version of sudo with Mac OS X from the beginning, but
while the version included in OS X has been based on an official sudo release
tarball it always has a few Apple-specific tweaks in it.  The earliest version
included by Apple was sudo-1.6.3p5 with Mac OS X 10.0.0.

As detailed in "Authentication bypass when clock is reset" sudo alert [2], sudo
versions 1.6.0 through 1.7.10p6 and sudo 1.8.0 through 1.8.6p6 inclusive are
affected by the problem.

The reason this problem is of particular concern on OS X is that most machines
running OS X will go through the standard Apple Setup Assistant that prompts on
initial use to create the first user account for the machine.  That account
will automatically be a member of the "admin" group and on OS X machines, the
"admin" group automatically has sudo access (the root account is disabled on OS
X unless explicitly enabled later by the user).

The problem arises in that members of the "admin" group may also change the
system clock time without needing to enter any password.  There's even a
command line utility to do this.

On 2013-09-12 Apple released a security update for OS X 10.7.5 that contains
an updated sudo with a fix for CVE-2013-1775 [1] and OS X 10.8.5 that also 
contains the same fix.  However, although a 10.6.8 security update was released
at the same time, it does NOT contain an updated sudo binary.  The updated sudo
version provided by the 10.7.5 security update and OS X 10.8.5 (as shown by
"sudo -V") is "1.7.4p6a".  As of this writing (2013-09-23) the Apple Open
Source version of sudo corresponding to "1.7.4p6a" has not yet been posted.

So any version of OS X prior to 10.7.5/10.8.5 whose admin user has run sudo for
any reason (and has not subsequently run "sudo -K" or added a workaround of
"timestamp_timeout 0" to the sudoers file) is vulnerable to a root access
exploit.  OS X 10.7.5 is also vulnerable unless the security update has been
installed.

-------
License
-------

The license is "BSD" + "MIT" as shown on Apple's Open Source site for the sudo
sources.  The LICENSE file from within the sudo-1.7.10p7.tar.gz file has been
included in this directory as LICENSE.txt for convenience.

Please take note of the license's disclaimer of liability for this software:

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

--------
Building
--------

The build script will extract, patch, configure and make a new sudo executable
suitable for use on the current system.

----------
Installing
----------

The build script emits instructions on how to install the new sudo executable
when it's finished building.  Doing so WILL REPLACE YOUR EXISTING sudo!!!

A backup of the previously installed sudo executable is highly recommended
before proceeding!!!

----------
References
----------

[1] http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2013-1775
[2] http://www.sudo.ws/sudo/alerts/epoch_ticket.html
