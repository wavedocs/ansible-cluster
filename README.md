ansible-cluster
===============

An example configuration for a web app using several servers

## First init phase
`ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook site.yml -i ansible_host -t init -k`
This step will setup your vms in a way that you can directly ssh into them because this is the basic requirement for ansible to work.

`SSH encountered an unknown error during the connection`
maybe wrong fingerprint in known_hosts

## Start
`ansible-playbook site.yml -i ansible_host --skip-tags=init`

## Available Tags
* init
* setup_db
* setup_db_cluster
* setup_web
* setup_load_balancer
* install_app
* update_app

# Before start
* add the public key of the machine from where you run ansible to `group_vars/all`

## Known issues
* add `-f 1` when running multiple (vagrant) machines on one host. Otherwise apt-get often exits with an error during update or install

## TODO
* `pg_master/tasks/main/add slave public key` don't use fix value. Make it generic
* `pg_slave/tasks/main/add master public key` don't use fix value. Make it generic
