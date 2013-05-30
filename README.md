# Vagrant files

Pelesend vagrant files to setup development environment (rvm, mysql, elasticsearch, redis).

## Preparation

~~~ sh
$ gem install vagrant
$ gem install chef
$ gem install librarian-chef
~~~

## Installation

~~~ sh
$ librarian-chef install
$ vagrant up
~~~

## MySQL access from host

1) with Sequel Pro

MySQL address: 10.0.2.15
user: 'root', password: 'password'

SSH address: 10.255.255.10
user: 'vagrant', password: 'vagrant'