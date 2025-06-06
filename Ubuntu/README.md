# Install Zabbix Agent2 on Ubuntu
Repositories for teaching purposes at SPOS DK

![Ubuntu and ZabbixAgent2 OSY AI](../Images/osy-Ubuntu-ZabbixAgent2.webp)

Repository pro vyuku na SPOS DK

## Automatická instalace Zabbix Agent2 na OS Linux Ubuntu

- Vagrantfile obsahuje sekci pro aplikaci příkazů pro instalaci monitorovacího
[Zabbix Agent2](https://www.zabbix.com/).

### Instalace Zabbix Agent2

```console
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest+ubuntu22.04_all.deb
dpkg -i zabbix-release_latest+ubuntu22.04_all.deb

apt-get update
apt-get install -y zabbix-agent2 zabbix-agent2-plugin-*

systemctl enable zabbix-agent2
systemctl start zabbix-agent2
```

### Konfigurace Zabbix Agent2

```console
joe /etc/zabbix/zabbix_agent2.conf
...
Hostname=ubuntu-8e714c18
Server=enceladus.pfsense.cz
ServerActive=enceladus.pfsense.cz
Timeout=30
HostMetadata=SPOS

systemctl restart zabbix-agent2
```
...

# Změny ve Vagrantfile
ubuntu.vm.network "private_network", ip: "192.168.1.3", 

# Změny v Configure-zabbix-agent2
### Nastav systémový hostname
echo "$SHORT_HOSTNAME" | sudo tee /etc/hostname
<p>
sudo hostnamectl set-hostname "$SHORT_HOSTNAME"
<p>
if grep -q "^HostMetadata=" /etc/zabbix/zabbix_agent2.conf; then
<p>
    sudo sed -i "s/^HostMetadata=.*/HostMetadata=SPOS/" /etc/zabbix/zabbix_agent2.conf
    <p>
else
<p>
    echo "HostMetadata=SPOS" | sudo tee -a /etc/zabbix/zabbix_agent2.conf

# Změny v install-zabbix-agent2
sudo apt-get install -y net-tools wget gnupg2
<p>
wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_7.0-1+ubuntu22.04_all.deb

