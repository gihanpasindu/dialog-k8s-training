```
yum update
yum install haproxy -y
yum install policycoreutils-python
setsebool -P haproxy_connect_any=1
```

Copy the contents of 02-haproxy.cfg to /etc/haproxy/haproxy.cfg 
test if the config is okay
```haproxy -f /etc/haproxy/haproxy.cfg -c```

Enable stats port

```
sudo semanage port --add --type http_port_t --proto tcp 7000
firewall-cmd --permanent --add-port=7000/tcp
```

```
systemctl enable haproxy
systemctl start haproxy
systemctl status haproxy
```

 