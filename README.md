# README

## Provision vuln vm's

```bash
openstack stack create mystack \
    -t template.yaml \
    -e env.yaml \
    --parameter image=mrRobot \
    --parameter count=5
```

## Create images from vulnhub

1. Download an image from vulnhub. For example: https://www.vulnhub.com/entry/mr-robot-1,151/

```bash
# Unpack ova
# https://opentox.github.io/installation/2012/08/02/converting-ova-images-to-kvm
tar -xvf mrRobot.ova
```

```bash
# Convert vmdk to raw disk
# https://docs.openstack.org/image-guide/convert-images.html
qemu-img convert -f vmdk -O raw mrRobot-disk1.vmdk mrRobot.raw
```

```bash
# Create image
openstack image create \
  --container-format bare \
  --disk-format raw \
  --private \
  --file mrRobot.raw \
  mrRobot
```