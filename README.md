# Vagrant-Ansible-Laravel #

Ansible provisioning of the Vagrant box for multiple Laravel projects.

That setup is heavily inspired by [https://github.com/hashbangcode/vlad](https://github.com/hashbangcode/vlad).

## Prerequisites ##

1. Linux or Mac
2. [Vagrant](https://www.vagrantup.com/downloads.html)
3. [Ansible](http://docs.ansible.com/intro_installation.html)

## Setup steps ##

1. Copy `provision/example.settings.yml` to `provision/settings.yml`

    `cd provision && cp example.settings.yml settings.yml`

2. Open `settings.yml` with your favorite editor.

  * Provide your details for git setup.
  * Change the box IP address (if needed).
  * Change to box name to your liking.
  * Set the amount of RAM for the box (MB).

**Note**: README is being updated. Provisioning script is in development.
