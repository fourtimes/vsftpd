vsftpd
-------
_Firstly , we have to implement the vsftpd installation and configuration. we need to follow the below command_

```sh
# Install the vsftpd packages
sudo apt update 
sudo apt install vsftpd -y

# create the new user
sudo adduser ashli # password - Password@123

# Create a directory for user and document root
sudo mkdir -p /etc/vsftpd/users /var/www/html/demo

# give the owner permission of new user
sudo chown -R ashli:ashli /var/www/html/demo

# give the local root
echo "local_root=/var/www/html/demo" | sudo tee -a /etc/vsftpd/users/ashli

# restrict the users at root level
echo "ashli" | sudo tee /etc/vsftpd.chroot_list
```
_Add the configuration file for vstfpd_
```sh
# sudo vim /etc/vsftpd.conf
listen=YES
listen_ipv6=NO
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
dirmessage_enable=YES
use_localtime=YES
xferlog_enable=YES
connect_from_port_20=YES
xferlog_file=/var/log/vsftpd.log
xferlog_std_format=NO
idle_session_timeout=600
data_connection_timeout=120
ascii_upload_enable=YES
ascii_download_enable=YES
ftpd_banner=Welcome to RADIANT FTP service.
chroot_local_user=YES
chroot_list_enable=NO
user_config_dir=/etc/vsftpd/users
allow_writeable_chroot=YES
secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
ssl_enable=NO
chroot_list_file=/etc/vsftpd.chroot_list
userlist_enable=YES
userlist_file=/etc/vsftpd.chroot_list
userlist_deny=NO
pasv_enable=YES
pasv_min_port=64000
pasv_max_port=64321
port_enable=YES
pasv_address=3.6.88.147 #ec2 public ip
pasv_addr_resolve=NO
```
_After creating the configuration file, we need to start the service and check the status of the service_
```sh
#  start the vsftpd service
sudo systemctl start vsftpd

#  status of vsftpd service
sudo systemctl status vsftpd

# verify the configuration
sudo ss -tulpn | grep vsftpd

```
