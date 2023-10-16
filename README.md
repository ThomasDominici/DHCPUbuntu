# DHCPUbuntu

# Configuration réseau du serveur DHCP : 

- On va dans les paramètres de la machine
- Réseau
- Petit rouage en face d'éthernet
- IPv4
- On met l'adresse IP en manuel et on la renseigne, ici : 172.20.0.5/24
- On redémarre la machine


# Configuration du serveur DHCP : 

- on installe le serveur avec la commande suivante :
  ```Bash
  sudo apt-get install isc-dhcp-server
  ```

- On va ensuite configurer :
```Bash
sudo nano /etc/dhcp/dhcpd.conf
```

- On inscrit ensuite les lignes suivantes :
```Bash
default-lease-time 600;
max-lease-time 7200;
option subnet-mask 255.255.255.0;
option broadcast-address 172.20.0.255;
option routers 172.20.0.254;
option domain-name-servers 172.20.0.1, 172.20.0.2;
option domain-name "ubuntu-fr.lan";
option ntp-servers 172.20.0.254;

subnet 172.20.0.0 netmask 255.255.255.0 {
  range 172.20.0.10 172.20.0.20;
}
```

- On configure aussi le fichier par défaut :
```Bash
sudo nano /etc/default/isc-dhcp-server
```

- On y inscrit : 
```Bash
INTERFACESv4="et0"
```


# Pour une adresse IP fixe : 

```Bash
sudo nano /etc/dhcp/dhcpd.conf
```
On inscrit : 

```Bash
host client1 {
hardware ethernet 4c:bb:58:9c:f5:55;
fixed-address 172.20.0.10;
}
```


