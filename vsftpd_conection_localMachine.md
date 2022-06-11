# vsftpd creation in local machine

```bash
# Install the vsftpd packages
sudo apt update && apt install vsftpd -y

# create the new user
sudo useradd -m -s /bin/bash ashli

#  set the password of new user
echo "ashli:password" | sudo chpasswd

# Create a directory
sudo mkdir -p /etc/vsftpd/users /var/www/html/fourtimes.ml

# give the owner permission of new user
sudo chown -R ashli:ashli /var/www/html/fourtimes.ml

# give the local root
echo "local_root=/var/www/html/fourtimes.ml" | sudo tee -a /etc/vsftpd/users/ashli

# give the change root
echo "ashli" | sudo tee /etc/vsftpd.chroot_list

# Create a configuration file in vsftpd
vim /etc/vsftpd.conf

add this content in vsftpd.conf file:
-------------------------------------
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
ftpd_banner=Welcome to fourtimes.ml FTP service.
chroot_local_user=NO
chroot_list_enable=YES
user_config_dir=/etc/vsftpd/users
allow_writeable_chroot=YES
secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
ssl_enable=NO
chroot_list_file=/etc/vsftpd.chroot_list

#  start the vsftpd service
sudo systemctl start vsftpd

#  status of vsftpd service
sudo systemctl status vsftpd
```
