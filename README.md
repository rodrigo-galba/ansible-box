# Ansible-Vagrant-Box

Configures a development environment for Ruby on Rails development. It will have the following main components:

- [RVM] - Ruby Version Manager (user_installs with Ruby 2.3.x)
- [MySQL] - The world's most popular open source database
- [Postgresql] - The world's most advanced open source database.
- [Node.js] - JavaScript runtime built on Chrome's V8 JavaScript engine
- [Puma] - A modern, concurrent web server for Ruby
- [Nginx] - Flawless application delivery for the modern web
- [Ansible] - Automation for everyone
- [Redis] - in-memory data structure store, used as a database, cache and message broker
- [RabbitMQ] - the most widely deployed open source message broker
- [Mailcatcher] - Catches mail and serves it through a dream

Provision requirements on Linux:
```sh
sudo apt-get install nfs-kernel-server
```

You can change the ruby version, just open the playbook.yml and change the
variable ```{ruby}```.

## Installation
##### Mac OS X

```sh
brew install ansible
brew cask install vagrant
brew cask install virtualbox
```

##### On Linux

Install packages:
- Ansible
- Vagrant
- VirtualBox

You are good to go, just run:
```
vagrant up --provision
```

## Usage

- Redis

```sh
redis-cli -a secret
ping
```

- RabbitMQ

Go to: http://localhost:15672 and use:
> username: `user2`
> password: `secret`

- Mailcatcher

Go to: http://localhost:1080

## License and Author
MIT
**Free Software, Yeah!**

Author:: Rodrigo Galba ([@rgalba](http://twitter.com/rgalba))

[RVM]: <https://rvm.io>
[Ansible]: <https://www.ansible.com>
[Postgresql]: <https://www.postgresql.org>
[MySQL]: <https://www.mysql.com>
[Node.js]: <https://nodejs.org/en/>
[Puma]: <http://puma.io>
[Nginx]: <https://www.nginx.com>
[RabbitMQ]: http://www.rabbitmq.com/
[Mailcatcher]: https://mailcatcher.me/
[Redis]: https://redis.io/
