# boxcutter/ubuntu

Use boxcutter/ubuntu templates 

## Clone boxcutter/ubuntu from Github

```sh
mkdir -p ~/projects1/boxcutter
cd ~/projects1/boxcutter

git clone https://github.com/boxcutter/ubuntu.git

cd ubuntu
```

## Modify json script to match the latest download location and create the vagrant box

The ubuntu18.04.json and ubuntu18.04-desktop.json tend to get out of date.
Edit ubuntu18.04.json to match the latest download location and update the SHA256 Sum.

### Build generic ubuntu box

```sh
packer build -only=virtualbox-iso -var-file=ubuntu1804.json ubuntu.json
```

It will take a long while to build it. Wait patiently...

### Build desktop ubuntu box

```sh
packer build -only=virtualbox-iso -var-file=ubuntu1804.json ubuntu.json
```

It will take a long while to build it. Wait patiently...

## Verify that the build is good and ready for use

### Prepare the box

```sh
mkdir -p ~/projects1/boxcutter_verify
cd ~/projects1/boxcutter_verify

vagrant box list


vagrant box add --name boxcutter/ubuntu1804-0.1.0 ~/projects1/boxcutter/ubuntu/box/virtualbox/ubuntu1804-0.1.0.box

vagrant box add --name boxcutter/ubuntu1804-desktop-0.1.0 ~/projects1/boxcutter/ubuntu/box/virtualbox/ubuntu1804-desktop-0.1.0.box

vagrant box list
```

Example output:

```sh
nvidia@develmachine2:~/projects1/boxcutter_verify$ vagrant box add --name boxcutter/ubuntu1804-0.1.0 ~/projects1/boxcutter/ubuntu/box/virtualbox/ubuntu1804-0.1.0.box
==> box: Box file was not detected as metadata. Adding it directly...
==> box: Adding box 'boxcutter/ubuntu1804-0.1.0' (v0) for provider: 
    box: Unpacking necessary files from: file:///home/nvidia/projects1/boxcutter/ubuntu/box/virtualbox/ubuntu1804-0.1.0.box
==> box: Successfully added box 'boxcutter/ubuntu1804-0.1.0' (v0) for 'virtualbox'!
```

```sh
nvidia@develmachine2:~/projects1/boxcutter_verify$ vagrant box add --name boxcutter/ubuntu1804-desktop-0.1.0 ~/projects1/boxcutter/ubuntu/box/virtualbox/ubuntu1804-desktop-0.1.0.box
==> box: Box file was not detected as metadata. Adding it directly...
==> box: Adding box 'boxcutter/ubuntu1804-desktop-0.1.0' (v0) for provider: 
    box: Unpacking necessary files from: file:///home/nvidia/projects1/boxcutter/ubuntu/box/virtualbox/ubuntu1804-desktop-0.1.0.box
==> box: Successfully added box 'boxcutter/ubuntu1804-desktop-0.1.0' (v0) for 'virtualbox'!
```


### Initialize and run the box

For ubuntu1804-0.1.0

```sh
mkdir -p ~/projects1/boxcutter_verify/boxcutter-ubuntu1804-0.1.0
cd ~/projects1/boxcutter_verify/boxcutter-ubuntu1804-0.1.0

# Initialize box
vagrant init boxcutter/ubuntu1804-0.1.0

# Start it
vagrant up

# Login
vagrant ssh
```

For ubuntu1804-desktop-0.1.0

```sh
mkdir -p ~/projects1/boxcutter_verify/boxcutter-ubuntu1804-desktop-0.1.0
cd ~/projects1/boxcutter_verify/boxcutter-ubuntu1804-desktop-0.1.0

# Initialize box
vagrant init boxcutter/ubuntu1804-desktop-0.1.0

# Start it
vagrant up

# Login
vagrant ssh
```
