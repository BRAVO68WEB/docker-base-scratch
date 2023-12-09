# Docker Image from Scratch

This is a simple example of how to create a Docker image from scratch. The image is based debian and write a simple script with two commands: `echo OK!` and `lsb_release -a`.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [debootstrap](https://wiki.debian.org/Debootstrap)

### Ubuntu/Debian

```bash
sudo apt install debootstrap
curl https://get.docker.com | sudo bash -
```

### Arch Linux

```bash
sudo pacman -S extra/debootstrap extra/docker
```

## Downloading the image

```bash
sudo debootstrap buster buster
```

## Customizing the image

### Chroot into the image

```bash
sudo chroot buster /bin/bash
```

### Update the image

```bash
apt update -y && apt upgrade -y
```

### Install the necessary packages

```bash
apt-get install -y lsb-release
```

### Clean the image

```bash
apt-get clean all
```

### Create the script

```bash
echo "echo OK!" > /root/script.sh
echo "lsb_release -a" >> /root/script.sh
```

### Make the script executable

```bash
chmod +x /root/script.sh
```

### Exit the image

```bash
exit
```

## Creating the image

```bash
sudo tar -C buster -c . | sudo docker import - buster
```

## Running the image

```bash
sudo docker run -it buster /root/script.sh
```

## References

- [https://docs.docker.com/engine/reference/commandline/import/](https://docs.docker.com/engine/reference/commandline/import/)
- [https://docs.docker.com/develop/develop-images/baseimages/](https://docs.docker.com/develop/develop-images/baseimages/)
- [https://docs.docker.com/develop/develop-images/baseimages/#create-a-simple-parent-image-using-debootstrap](https://docs.docker.com/develop/develop-images/baseimages/#create-a-simple-parent-image-using-debootstrap)
