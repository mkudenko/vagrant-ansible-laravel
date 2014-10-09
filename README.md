# Vagrant-Ansible-Laravel #

Ansible provisioning of the Vagrant box for multiple Laravel projects. It is designed so that you don't need to have things like webserver or Composer installed on your local system. You'll be able to do everything from within the virtual box.

That setup is heavily inspired by [https://github.com/hashbangcode/vlad](https://github.com/hashbangcode/vlad) and [Laravel Homestead](http://laravel.com/docs/4.2/homestead).

## What's inside ##

* Ubuntu 14.04 64-bit
* Nginx
* PHP-FPM 5.6
* MySQL + Adminer
* Codeception + PhantomJS
* NodeJS + Bower + Grunt
* Composer + Laravel installer
* Git, Vim, Midnight Commander, etc.

Ruby, Sass, Compass are currently disabled. For some reason, Ansible has troubles installing gems.

## Prerequisites ##

1. Linux or Mac
2. [Vagrant](https://www.vagrantup.com/downloads.html)
3. [Ansible](http://docs.ansible.com/intro_installation.html)
4. [Virtual Box](https://www.virtualbox.org/wiki/Downloads)

## Setup steps ##

1. Copy `provision/example.settings.yml` to `provision/settings.yml`

    `cd provision && cp example.settings.yml settings.yml`

2. Open `settings.yml` with your favorite editor.

  * Provide your details for git setup.
  * Pick a webserver hostname. Phpinfo will be available at this URL.
  * Setup virtual hosts. See **Virtual hosts** section
  * Change the box IP address (if needed).
  * Change to box name to your liking.
  * Set the amount of RAM for the box (MB).
  * Change any other settings, though default are usually sufficient.

3. Run `vagrant up`. You will be asked for your system password in the beginning and in the end of the installation.
4. Run `vagrant ssh` to login to your box. All sites folders are in `~/sites` derectory.

## Virtual hosts ##

You can have as many sites as you want on a single box.

    # Virtual hosts
    vhosts:
      - alias: first-project.local
        path: ~/projects/first_project
        db: project1
      - alias: second-project.local
        path: ~/projects/second_project
        db: project2

Your project folders must exist but shouldn't contain any code. You will create a new application or clone the existing one from within the virtual box.

Virtual hosts are updated every time you run `vagrant up` or `vagrant reload`.

## Creating an application ##

Assuming that you've already created a virtual host for your app `project.local`, go to `~/sites/project.local`.

Your application must reside in that folder, no subfolders.

    ~/sites/project.local/public/index.php

Open your browser and go to `project.local/`. Job done.
