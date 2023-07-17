#### EC2

```
chmod 400 LingKeyPair.pem
sudo su
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
systemctl status httpd
cd /var/www/html
```