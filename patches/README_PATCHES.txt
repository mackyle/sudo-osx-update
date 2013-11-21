===========================
Apple Specific sudo Patches
===========================

The Apple version of the sudo sources can be found on the Apple Open Source
site at http://opensource.apple.com/source/sudo/ in various subdirectories.

OS X version 10.4.11 and 10.5.8 uses sudo-28, OS X version 10.6.8 uses sudo-46
and OS X version 10.8.4 uses sudo-67.  OS X 10.7.5+security update and OS X
10.8.5 use sudo-67.1 and OS X 10.9.0 uses sudo-72.

The Apple sudo-16, sudo-17 and sudo-23 versions conveniently provide a set of
patches (in the patches subdirectory) against an official sudo release tarball.
The other Apple versions do not.

The patches in this directory were culled from sudo-28, sudo-46 and sudo-67
by examining the contents of the patches subdirectory (sudo-28) and/or
performing diffs against the related official sudo release tarball.  They were
then adjusted for use with the official sudo-1.7.10p7 release tarball.

The top-level build script will automatically apply all these patches before
building sudo.

Here's a summary of the patches provided:


0001-Add-BSM-auditing-support.patch.txt:

Most all of the Apple BSM auditing changes/fixes have been picked up by the
official sudo source releases in 1.7.10p7, however this patch does add a check
to prevent calling au_to_exec_args with a NULL pointer and two additional
audit_failure calls.


0002-Remove-sudoedit-and-sudoreplay-references.patch.txt:

This is a cosmetic patch.  The Apple version of sudo includes neither sudoedit
nor sudoreplay.  This patch removes references to those from the man page and
avoids installing them.


0003-Remove-login_cap-reference-from-man-page.patch.txt:

Another cosmetic patch.  OS X has no login_cap functions so this patch removes
the reference to such from the man page.


0004-Disable-tty_tickets-by-default.patch.txt

Not strictly required except to match existing OS X behavior.  This patch
changes the tty_tickets default from on to off (and updates the man page).


0005-Allow-admin-group-by-default.patch.txt

On OS X the root user is normally not enabled and the first user created is
made a member of the admin group which must be able to run sudo.  This patch
adds "%admin	ALL=(ALL) ALL" to the default sudoers file.


0006-Friendlier-warning-on-first-usage.patch.txt

The Apple management prefers a different warning on first use of sudo.  This
patch makes it so.  Only required to match pre-existing Apple sudo behavior.


0007-Clean-the-environment.patch.txt

The Apple version of sudo keeps both HOME and MAIL environment variables by
default and has an explicit (and somewhat smaller) list of environment
variables in the default sudoers file.  Only required to mirror pre-existing
Apple sudo behavior.


0008-Restore-sudoers-samples.patch.txt

The Apple version of sudo includes some additional "Samples" lines that are
commented out in the example sudoers file.  This patch restores them and is
strictly cosmetic.


0009-Do-not-close-fds-on-OS-X.patch.txt

The Apple version of sudo prefers to set the close-on-exec flag for file
descriptors that need to be closed when running the sudo child executable
rather than actually closing them in the parent process.  This may even be
Apple internal bug number 6497333 judging by the patch.  Presumably this patch
corrects some undesirable failure on OS X.  Also changes the location to read
the current list of open file descriptors from "/proc/self/fd" to "/dev/fd".


0010-Handle-EINTR-when-calling-tcsetattr.patch.txt

Apparently on OS X tcsetattr can return EINTR.  This patch handles this error
by retrying the call.  Only the tcsetattr in term_restore and term_noecho get
this treatment though.  Presumably this addresses an OS X specific failure.


0011-Do-not-quote-possible-meta-characters.patch.txt

With sudo versions 1.7.0-1.7.2*, using "sudo -s 'echo ${PWD+abc}'" will output
the string "abc".  Prior sudo versions do not invoke the shell with "-c" and
later versions escape anything that could possibly be a shell meta character by
preceding it with a '\' character.  When Apple switched to an sudo based on the
official sudo 1.7.4p6 release they included a patch to revert to the
1.7.0-1.7.2* behavior.  This patch implements that change in order to maintain
compatibility with Apple sudo behavior.  This really only matters if both the
sudo "-s" option is given AND following arguments are given.  This would seem
to likely be a corner case and is only required to mirror pre-existing Apple
sudo behavior.


0012-Allow-without-iologdir-configure-option-to-build.patch.txt

Even though the INSTALL option describes the --without-iologdir configure
option, attempting to use it causes exec.c to fail to build.  This patch
corrects the problem so "configure --without-iologdir" can be used
successfully.  This is a general fix that is not specific to OS X.
