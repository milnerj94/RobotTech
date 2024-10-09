I will continue to do my own research when I dont understand or am behind.

yum install httpd
systemctl start httpd
systemctl enable httpd
systemctl status httpd
firewall-cmd --permanent --add-service=http
firewall-cmd --reload
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache.key -out /etc/ssl/certs/apache.crt 
/etc/httpd/conf/httpd.conf:
<VirtualHost _default_:443>
    DocumentRoot "/var/www/html"
    ServerName your-server-name
 
    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/apache.crt
    SSLCertificateKeyFile /etc/ssl/private/apache.key
 
    <Directory "/var/www/html">
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>
</VirtualHost>
systemctl restart httpd
/etc/httpd/conf/httpd.conf
<FilesMatch "\.(log|cfg)$">
    Require all denied
</FilesMatch>
