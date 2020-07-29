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
sudo apt install openvpn
sudo openvpn --config stream.ovpn

#ALLOW SSH
#sudo iptables -A INPUT -d x.x.x.x -p tcp --dport 22 -j ACCEPT
```

# Bastion

## OpenVPN install:
```bash
curl -O https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh
chmod +x openvpn-install.sh
sudo ./openvpn-install.sh
sudo iptables -t nat -A PREROUTING -p tcp --dport 8554 -j DNAT --to-dest 18.234.228.182:8554
#sudo iptables -A POSTROUTING -t nat -p tcp -d 18.234.228.182 --dport 8554  -j MASQUERADE
```


## MISC
```bash
sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
sudo service ssh restart
sudo su --> passwd
ssh  -g -L 8554:35.232.81.205:8554 -f -N cloud_user_p_a2f9a4af@35.232.81.205

sudo apt install tcptrack
sudo tcptrack -i eth0 port 8554
```
