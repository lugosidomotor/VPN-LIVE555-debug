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

#Allow SSH
#sudo iptables -A INPUT -d x.x.x.x -p tcp --dport 22 -j ACCEPT
```

# Bastion

## OpenVPN install:
```bash
curl -O https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh
chmod +x openvpn-install.sh
sudo ./openvpn-install.sh

sudo sysctl -w net.ipv4.ip_forward=1

sudo iptables -t nat -A PREROUTING -p tcp --dport 8554 -j DNAT --to-dest x.x.x.x:8554
#sudo iptables -A POSTROUTING -t nat -p tcp -d x.x.x.x --dport 8554  -j MASQUERADE

#sudo iptables -L -x -n -v -t nat
```


## MISC
```bash
#Allow SSH with Password
sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
sudo service ssh restart
sudo su --> passwd

#SSH tunneling
ssh  -g -L 8554:x.x.x.x:8554 -f -N user@x.x.x.x

sudo apt install tcptrack
sudo tcptrack -i eth0 port 8554
```

```bash
port 1194
proto udp
dev tun
user nobody
group nogroup
persist-key
persist-tun
keepalive 10 120
topology subnet
server 10.8.0.0 255.255.255.0
ifconfig-pool-persist ipp.txt
push "dhcp-option DNS 172.31.0.2"
push "redirect-gateway def1 bypass-dhcp"
dh none
ecdh-curve prime256v1
tls-crypt tls-crypt.key 0
crl-verify crl.pem
ca ca.crt
cert server_ghY5fjjEZ8kDCtK4.crt
key server_ghY5fjjEZ8kDCtK4.key
auth SHA256
cipher AES-128-GCM
ncp-ciphers AES-128-GCM
tls-server
tls-version-min 1.2
tls-cipher TLS-ECDHE-ECDSA-WITH-AES-128-GCM-SHA256
client-config-dir /etc/openvpn/ccd
status /var/log/openvpn/status.log
verb 3
```
