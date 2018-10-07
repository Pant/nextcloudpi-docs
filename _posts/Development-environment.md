Development environment
=======================

## Using docker

In order to facilitate development, the x86 NextCloudPi docker container can be used.

Install docker and docker-compose and

```
git clone https://github.com/nextcloud/nextcloudpi.git
cd nextcloudpi
docker-compose -f docker-compose-ncpdev.yml up
```

We can now access the interface at `https://localhost:4443`. 

We can start working in the folder `ncp-web` from the repo and refresh the browser to see the changes live.

In the same way, we can edit any NCP option in the folder `nextcloudpi-config.d`.

Changes can be made directly on the repo, no more copying files back and forth!

## Using QEMU

Follow [this guide](https://ownyourbits.com/2017/02/06/raspbian-on-qemu-with-network-access/)

```
sudo ./qemu-pi.sh NextCloudPi_03-13-17.img
```

## Using VirtualBox

Follow [this guide](http://ediy.com.my/index.php/blog/item/52-virtualbox-raspberry-pi-emulator)

## Using virt-manager

-- help needed --