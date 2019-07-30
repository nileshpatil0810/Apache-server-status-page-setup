# Apache-server-status-page-setup
How to setup http://domain.com/server-status on Apache server?

Apache (Ubuntu OS)
Edit file /etc/apache2/mods-available-> status.conf
<Location /server-status>
        SetHandler server-status
        Order allow,deny
        Allow from 122.170.1.34
</Location>

Apache (Linux-CentOS)
Edit file /etc/httpd/conf -> httpd.conf (or use any virtualhost conf file)

LoadModule status_module modules/mod_status.so 
<Location /server-status> 
    SetHandler server-status 
    Order allow,deny 
    Allow from 122.170.1.34
</Location>     

If you would like to make it as public then use following code
Allow from all 
Use refresh time parameter in request to get automatically refresh after that time like https://domain.com/server-status?refresh=5

Error:
If you are facing issue like http://domain.com/server-status URL redirect on http://domain.com/ then add following line in .htaccess of domain root
RewriteEngine On
RewriteCond %{REQUEST_URI} !^/server-status

Advantage
This is easiest tool to trace which process currently consuming more memory on Apache
