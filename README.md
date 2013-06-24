# Vagrant

Vagrant provides easy to configure, reproducible, and portable work environments (rvm, mysql, elasticsearch, redis, etc).

## Getting started

### Prerequisites:

1. Install standard ruby stack (Git, Ruby, RubyGems) RailsInstaller: http://www.railsinstaller.org/ (or [How to install Ruby on Rails in Ubuntu on the Sudobits Blog](http://blog.sudobits.com/2012/05/02/how-to-install-ruby-on-rails-in-ubuntu-12-04-lts/) if you on Linux)
2. Install VirtualBox: https://www.virtualbox.org/wiki/Downloads
3. Install Vagrant: http://www.vagrantup.com/ (We require Vagrant 1.1.2+ or later)
4. Open a terminal
5. Clone the project: `git clone https://github.com/pelesend/project_name.git`
6. Enter the project directory: `cd project_name`
7. Install Chef: `gem install chef`
8. Install Librarian (bundler for chef cookbooks): `gem install librarian-chef`

### First time run

Install required cookbooks for chef:
~~~ sh
$ librarian-chef install
~~~

Then boot up VM:
~~~ sh
$ vagrant up
~~~

Vagrant will prompt you for your admin password. This is so it can mount your local files inside the VM for an easy workflow.
(The first time you do this, it will take a while as it downloads the VM image and installs it.)

**Note to All users**: This is very important to sync project folder via NFS, because default shared folder implementations (such as VirtualBox shared folders) have high performance penalties.
[Additional info about NFS on Vagrant Docs](http://docs.vagrantup.com/v2/synced-folders/nfs.html)

**Note to Windows users**: NFS folders do not work on Windows hosts. Vagrant will ignore your request for NFS synced folders on Windows.

**Note to Linux users**: Your Project directory cannot be on an ecryptfs mount or you will receive an error: `exportfs: /home/your/path/to/project does not support NFS export`

**Note to OSX/Linux users**: Vagrant will mount your local files via an NFS share. Therefore, make sure that NFS is installed or else you'll receive the error message:

```
Mounting NFS shared folders failed. This is most often caused by the NFS
client software not being installed on the guest machine. Please verify
that the NFS client software is properly installed, and consult any resources
specific to the linux distro you're using for more information on how to
do this.
```

## Using

### MySQL access from host

1) with Sequel Pro

MySQL address: 10.0.2.15
user: 'root', password: 'password'

SSH address: 10.255.255.10
user: 'vagrant', password: 'vagrant'