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


vagrant box add --name boxcutter/ubuntu1804-0.1.0 ~/projects1/boxcutter/ubuntu/box/ubuntu1804-0.1.0.box

vagrant box add --name boxcutter/ubuntu1804-desktop-0.1.0 ~/projects1/boxcutter/ubuntu/box/ubuntu1804-desktop-0.1.0.box

vagrant box list
```

### Initialize and run the box

For ubuntu1804-0.1.0

```sh
# Initialize box
vagrant init boxcutter/ubuntu1804-0.1.0

# Start it
vagrant up

# Login
vagrant ssh
```

For ubuntu1804-desktop-0.1.0

```sh
# Initialize box
vagrant init boxcutter/ubuntu1804-desktop-0.1.0

# Start it
vagrant up

# Login
vagrant ssh
```
