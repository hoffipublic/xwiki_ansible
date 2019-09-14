# Ansible runboot to install xwiki

## xwiki installation via ansible

### preparing steps on ansible machine

if a local vagrant installation:  `vagrant plugin install vagrant-hostmanager`

install referenced ansible-galaxy modules to $HOME/.ansible/roles/
- `ansible-galaxy install idealista.java_role`
- `ansible-galaxy install geerlingguy.postgresql`
- `ansible-galaxy install cscfi.jetty`

`vagrant up`

after first time creation of the vm, to be able for vagrant to ssh to it, you have to one time do this `vagrant ssh xwiki1` manual and then kick off the ansible provisioning again by either `vagrant up --provision` or running the runbook directly `ANSIBLE_FORCE_COLOR=true ansible-playbook -vv --inventory-file=inventory-LOCAL.ini xwiki_runbook.yml | sed 's/\\n/\
/g'
`

to see how jetty is configured issue `java -jar start.jar --list-config` (or better see directly with `ps -aef | grep jetty`)

## configure xwiki after install (on farm)

browse to xwiki (e.g. http://10.0.0.49:8080)

follow the instructions...

extendsion I prefer to install:

- Diagram Application
- Markdown Syntax

optional:

- Office365 Integration
