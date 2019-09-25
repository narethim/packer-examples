# packer-examples

This example will build a vagrant box using packer.
This version enhanced the original version of an article [Create simple CentOS 7 Virtualbox with Packer](https://softwaretester.info/create-simple-centos-7-virtualbox-with-packer).

## Prerequisite

* A bare metal machine
* VirtualBox installed

## Steps to build it

### Clone the repository

```sh
cd ~/projects

git clone https://github.com/narethim/packer-examples.git

cd packer_examples/example_2
```

### Build vagrant box

```sh
# Validate json file
packer validate example.json

# create box
packer build example.json
```

After a successful build the box will be located at `builds/virtualbox-centos7.box`

## The differences and enhancements

Changes in file `http/ks.cfg'

```cfg
rootpw --plaintext packer
user --name frank --password=Test123
```

changed to

```cfg
rootpw --plaintext vagrant
user --name vagrant --password=vagrant
```

Changes in file `example.json'

```json
"ssh_username": "root",
"ssh_password": "packer",
```

changed to

```json
"ssh_username": "vagrant",
"ssh_password": "vagrant",
```

Add `post-processors` section as follow:

```json
"post-processors": [
    [
        {
            "output": "builds/{{.Provider}}-centos7.box",
            "type": "vagrant"
        }
    ]
]

```

## Verify the vagrant box

### Prepare the box

```sh
cd ~/projects1
mkdir -p packer_examples_verify/example_2

cd packer_examples_verify/example_2

vagrant box list

vagrant box add -h

vagrant box add --name example_2/centos7 ~/projects1/packer-examples/example_2/builds/virtualbox-centos7.box

vagrant box list

```

### Initialize and run the box

```sh
# Initialize box
vagrant init example_2/centos7

# Start it
vagrant up

# Login
vagrant ssh
```

Example outputs:

```sh

# Login
nvidia@develmachine2:~/projects1/packer_examples_verify/example_2$ vagrant ssh
vagrant@127.0.0.1's password:
Last login: Wed Sep 25 17:04:47 2019 from gateway
[vagrant@localhost ~]$

```
