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

## Getting Started ##
 0. Create a new compute instance, `ubuntu-16.04` version `201704031` <https://my.joyent.com/main/#!/compute>. Minimum recommended profile is `g4-highcpu-1G`.
 0. Copy instance IP address, open ansible `deploy/playbooks/inventory` file in editor. Un-comment sample row and paste new IP address into `calliope_build_servers` section. Choose new ansible become password if desired and edit as necessary.
 0. Connect as root to newly created server: `ssh root@37.153.111.88`. Note that root authentication in Joyent cloud is automatically performed via public key stored in Joyent profile.
 0. Create new non-root account for build user: `cbuild` (must be same as the `ansible_ssh_user` in Ansible `inventory`): `adduser cbuild`. Use the password from the Ansible `ansible_become_pass` variable in the `inventory` file.
 0. Add build user to the sudo group (so we can install packages): `usermod -a -G sudo cbuild`.
 0. Create `.ssh` directory for new cbuild user: `mkdir /home/cbuild/.ssh`.
 0. Create `authorized_keys` file with your public key for cbuild user (run on local machine): `scp ~/.ssh/id_rsa.pub root@37.153.111.88:/home/cbuild/.ssh/authorized_keys`.
 0. Set ownership of `.ssh` directory: `chown -R cbuild:cbuild /home/cbuild/.ssh`
 0. Logout of root session from remote.
 0. Verify you can log in as cbuild user without needing password: `ssh cbuild@37.153.111.88`.
 0. Verify sudo works: `sudo whoami`. You will need to enter the ansible become password when using sudo.
 0. Run ansible playbook: `ansible-playbook -v -i inventory calliope-build.yml`
 0. Build MicroPython. **To be automated next**
 0. Copy binary files from build server to local machine: `scp cbuild@37.153.111.88:~/microbit_build/micropython/build/bbc-microbit-classic-gcc-nosd/source/microbit-micropython.* .`
 0.
