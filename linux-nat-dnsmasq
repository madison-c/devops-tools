setenforce 0
sed -i '/SELINUX=enforcing/s/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config 
yum -y install git vim wget
systemctl enable firewalld
systemctl start firewalld
yum -y install bash-completion
source /etc/profile
nmcli con add con-name ens37 ifname ens37 type ethernet ip4 172.16.1.1/24
nmcli connection up ens37

firewall-cmd --get-active-zones 
nmcli  connection modify ens37  connection.zone internal
firewall-cmd --get-active-zones 
nmcli  connection modify ens33  connection.zone external
firewall-cmd --get-active-zones 
firewall-cmd --zone=external --add-masquerade --permanent 
firewall-cmd --reload 
firewall-cmd --zone=external --query-masquerade 

sysctl -w net.ipv4.ip_forward=1
cat /etc/sysctl.conf 
vim /etc/sysctl.conf
cat /proc/sys/net/ipv4/ip_forward 
firewall-cmd --direct --add-rule ipv4 nat POSTROUTING 0 -o ens33 -j MASQUERADE 
firewall-cmd --direct --add-rule ipv4 filter FORWARD 0 -i eth0 -o ens33 -j ACCEPT 
firewall-cmd --direct --add-rule ipv4 filter FORWARD 0 -i ens37 -o ens33 -j ACCEPT 
firewall-cmd --direct --add-rule ipv4 filter FORWARD 0 -i ens33 -o ens37 -m state --state RELATED,ESTABLISHED -j ACCEPT

firewall-cmd --list-all --zone=external
iptables -L
