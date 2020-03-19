# DirectAdmin-1.59.5 - Installation Successful
# P/s: Chú ý bản này chỉ chạy được trên Centos 7 64bit
# Cài đặt:
```
 yum -y install nano wget perl
 wget https://raw.githubusercontent.com/puarudz/DirectAdmin-1.59.5/master/setup.sh
 chmod +x setup.sh
 ./setup.sh
```
# Nhập ID và lic id con số bất kỳ bạn thích

# Chú ý sau khi cài xong sẽ ko run được thì khai báo port cho nó lệnh
```
firewall-cmd --zone=public --add-port=2222/tcp --permanent
firewall-cmd --zone=public --add-port=21/tcp --permanent
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --zone=public --add-port=25/tcp --permanent
firewall-cmd --reload
systemctl restart directadmin
cd /usr/local/directadmin/conf/
service directadmin stop
rm -rf /usr/local/directadmin/conf/license.key
wget -O /usr/local/directadmin/conf/license.key https://raw.githubusercontent.com/puarudz/DirectAdmin-1.59.5/master/license.key
chmod 600 /usr/local/directadmin/conf/license.key
chown diradmin:diradmin /usr/local/directadmin/conf/license.key
ifconfig eth0:100 103.127.207.212 netmask 255.0.0.0 up
echo 'DEVICE=eth0:100' >> /etc/sysconfig/network-scripts/ifcfg-eth0:100
echo 'IPADDR=103.127.207.212' >> /etc/sysconfig/network-scripts/ifcfg-eth0:100
echo 'NETMASK=255.0.0.0' >> /etc/sysconfig/network-scripts/ifcfg-eth0:100
service network restart
/usr/bin/perl -pi -e 's/^ethernet_dev=.*/ethernet_dev=eth0:100/' /usr/local/directadmin/conf/directadmin.conf
service directadmin start
ifdown eth0:100
```
# Nếu license hết hạn, vui thì chỉ cần chạy lệnh sau:
# IF IPADDR in /etc/sysconfig/network-scripts/ifcfg-eth0:100 != 103.127.207.212 then EDIT TO 103.127.207.212

```
rm -rf /usr/local/directadmin/conf/license.key
wget -O /usr/local/directadmin/conf/license.key https://raw.githubusercontent.com/puarudz/DirectAdmin-1.59.5/master/license.key
chmod 600 /usr/local/directadmin/conf/license.key
chown diradmin:diradmin /usr/local/directadmin/conf/license.key
ifup eth0:100
systemctl restart directadmin
ifdown eth0:100
```
# Cách fix VPS không vào được mạng sau khi edit network :
```ifdown eth0:100```
