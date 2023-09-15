
**1. Install the vsftpd using the below url** 

https://github.com/fourtimes/vsftpd/blob/main/vsftpd-with-remoteuser.md

**2. vsftpd with SSL**

Install the openssl package
```sh
sudo apt-get update
sudo apt-get install openssl
```
Generate the ssl key
```sh
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/vsftpd.key -out /etc/ssl/certs/vsftpd.crt
```
adding the ssl configuration
```sh
# sudo nano /etc/vsftpd.conf
rsa_cert_file=/etc/ssl/certs/vsftpd.crt
rsa_private_key_file=/etc/ssl/private/vsftpd.key
ssl_enable=YES
allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES
ssl_tlsv1=YES
ssl_sslv2=NO
ssl_sslv3=NO
require_ssl_reuse=NO
ssl_ciphers=HIGH
```
Enable the Firewall Port
```sh
sudo ufw allow 21/tcp
```
Restart the service
```sh
sudo service vsftpd restart
```
