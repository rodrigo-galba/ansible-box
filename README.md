# Railsbox

Configures a development environment for Ruby on Rails development. It will have the following main components:

- [RVM] - Ruby Version Manager (user_installs with Ruby 2.3.x)
- [MySQL] - The world's most popular open source database
- [Postgresql] - The world's most advanced open source database.
- [Node.js] - JavaScript runtime built on Chrome's V8 JavaScript engine
- [Puma] - A modern, concurrent web server for Ruby
- [Nginx] - Flawless application delivery for the modern web
- [Ansible] - Automation for everyone

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