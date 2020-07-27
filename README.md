# Media Server

## live555 install:
```bash
git clone https://github.com/lugosidomotor/VPN-LIVE555-debug.git
tar -xJf ./VPN-LIVE555-debug/live555_linux.tar.xz
cd live555_linux/mediaServer/
sudo apt install make
sudo make install
live555MediaServer &
```

## OpenVPN install:
```bash

```

# Bastion

## OpenVPN install:
```bash

```

## VNC install:
```bash

```

## WireShark install:
```bash

```


## MISC
```bash
sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
sudo service ssh restart
sudo su --> passwd
ssh  -g -L 8554:35.232.81.205:8554 -f -N cloud_user_p_a2f9a4af@35.232.81.205
```
