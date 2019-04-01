https://www.youtube.com/watch?v=Vd2aLTZDLQg

##### Create a directory to host your site:
`sudo mkdir -p /var/www/btnhd.com/public_html`
##### 
##### Grant permissions to the folder you create:
`sudo chown -R $USER:$USER /var/www/btnhd.com/public_html`

##### Changing permission on the main root of the website folder:
`sudo chmod -R 755 /var/www`

##### Let’s create a dummy html page to test out our host server:
`nano /var/www/btnhd.com/public_html/index.html`
```HTML
<html>
<head>
<title>BTNHD SITE</title>
</head>
<body>
<h1>NICE!!! It’s Working!!!</h1>
</body>
</html>
```
##### Make a copy of the default virutal host file within Ubuntu and name it – using the site name so it can be easy to identified:
`sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/btnhd.com.conf`

##### Edit the new Virtual host file, we will be adding and changing the following in bold:
`sudo nano /etc/apache2/sites-available/btnhd.com.conf`
```
<VirtualHost *:80>
ServerAdmin info@btnhd.com
ServerName btnhd.com
ServerAlias www.btnhd.com
DocumentRoot /var/www/btnhd.com/public_html
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
##### We will need to enable the new virtual host file with the following command:
`sudo a2ensite btnhd.com.conf`

##### But, we also need to disable the default virtual host file within the Ubuntu server – we don’t want a conflict:
`sudo a2dissite 000-default.conf`

##### Enter the following command to restart apache server:
`sudo service apache2 restart`

##### This is an optional setup, but it’s good practice to do it and that’s setting up local host files to point to your site that you created above – we need to edit the “host” file:
`sudo nano /etc/hosts`
