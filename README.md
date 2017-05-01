# calliope-build
A build environment for the Calliope mini firmware

## Current Resources ##
 * Damien George on newlib version: *To fix the problem with newlib you'll need to revert to a known-working version (I use 2.4.0-3 from Arch Linux).  If you use Arch then you'll need to edit your /etc/pacman.conf file and add arm-none-eabi-newlib to the IgnorePkg line.  Then obtain arm-none-eabi-newlib-2.4.0-3-any.pkg.tar.xz for your architecture and use "pacman -Uarm-none-eabi-newlib-2.4.0-3-any.pkg.tar.xz" to downgrade.*
 * A project to create microbit dev based on Vagrant (ubuntu-16.04): <https://github.com/carlosperate/microbit-dev-env>
 * The bug encountered when using a newer (?) version of newlib: <https://github.com/bbcmicrobit/micropython/issues/363>
 
## Initial ideas ##
 * Create an Ansible script for configuring a build environment based on Ubuntu 16.04. This environment can leverage the existing work from the microbit Vagrant project.
 * Ubuntu build environment can be container based using a service such as Joyent Triton to make it easy to replicate.
 * The right version of newlib may need to be installed from source to compile the right gcc.
 
