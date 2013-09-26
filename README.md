# Vagrant Lab

## Initial Setup

Download and install the following on your workstation:

1. [VirtualBox][vb_site] (currently tested on version 4.2.4 on Mac)
2. [VirtualBox Oracle VM VirtualBox Extension Pack][vb_site] (optional)
3. [Vagrant][vagrant_site] (package install, version 1.1.0 or higher)
4. [vagrant-berkshelf plugin][vagrant_berkshelf] (needed to resolve and use cookbooks)
5. [vagrant-omnibus plugin][vagrant_omnibus] (needed to install Chef on the Vagrant VMs)

Now clone this project repo to your workstation.

All you should have to type in the project directory is:

```sh
$ ./script/bootstrap
```

Follow any directions given and possibly re-run the bootstrap script.

## Usage

### Starting The Jenkins Node

```sh
$ vagrant up jenkins
```

## Starting The Chef Server (Optional)

```sh
$ vagrant up chef
```

## Starting The Nexus Server

```sh
$ vagrant up nexus
```

### Starting The Entire Cluster

```sh
$ vagrant up
```


[bento_site]:   https://github.com/opscode/bento
[opscode_site]: http://www.opscode.com/
[vb_site]:      https://www.virtualbox.org/wiki/Downloads
[veewee_site]:  https://github.com/jedi4ever/veewee
[vagrant_site]: http://vagrantup.com/
[vagrant_berkshelf]: http://berkshelf.com/
[vagrant_omnibus]: https://github.com/schisamo/vagrant-omnibus
