
### Installation and configure hosts: https://www.digitalocean.com/community/tutorials/how-to-install-nagios-4-and-monitor-your-servers-on-ubuntu-16-04

After the installtion & setup done

![image](https://user-images.githubusercontent.com/24622526/44900118-46d20700-acf3-11e8-99f3-7ce337c4b4fc.png)

Stopping the server:

![image](https://user-images.githubusercontent.com/24622526/44900064-286c0b80-acf3-11e8-9217-a5bb4cb7e748.png)

Server Stopped:

![image](https://user-images.githubusercontent.com/24622526/44900092-3752be00-acf3-11e8-9ff4-df3899d80902.png)

Server Status in Nagios:

![image](https://user-images.githubusercontent.com/24622526/44899831-674d9180-acf2-11e8-81e6-d0a51677ead4.png)

Start the client server and wait for sometime (then refresh the nagios server in browser)

![image](https://user-images.githubusercontent.com/24622526/44899983-eba01480-acf2-11e8-9317-ff1e61660f71.png)

https://www.linkedin.com/pulse/container-monitoring-nagios-vinay-thakur/


---

## Step-1: Nagios Installtion on Ubuntu: 

##### Installtion steps in official page : https://support.nagios.com/kb/article/nagios-core-installing-nagios-core-from-source-96.html#Ubuntu


##### 1.1. Launch an "Ubuntu Server 16.04" in AWS.

##### 1.2. Connect to the machine

      sudo -i
      
      hostname NagiosServer
      
      echo NagiosServer > /etc/hostname OR vi /etc/hostname
      
      exit and connect to the machine again.
      
      
![image](https://user-images.githubusercontent.com/24622526/44909089-87d71500-ad0d-11e8-9a8e-718e8cd7244a.png)

    
##### 1.3. Install required dependencies

      sudo apt-get update
      sudo apt-get install -y autoconf gcc libc6 make wget unzip apache2 php libapache2-mod-php7.0 libgd2-xpm-dev
      
##### 1.4. Download Nagios

      cd /tmp
      wget -O nagioscore.tar.gz https://github.com/NagiosEnterprises/nagioscore/archive/nagios-4.4.1.tar.gz
      tar xzf nagioscore.tar.gz
      
##### 1.5. Compile

      cd /tmp/nagioscore-nagios-4.4.1/
      sudo ./configure --with-httpd-conf=/etc/apache2/sites-enabled
      sudo make all
      
##### 1.6. Create User And Group

      sudo make install-groups-users
      sudo usermod -a -G nagios www-data
      
##### 1.7. Install Binaries

      sudo make install

##### 1.8. Install Service / Daemon

      sudo make install-daemoninit

##### 1.9. Install Command Mode

      sudo make install-commandmode

##### 1.10. Install Configuration Files

      sudo make install-config

##### 1.10. Install Apache Config Files

      sudo make install-webconf
      sudo a2enmod rewrite
      sudo a2enmod cgi

##### 1.10. Configure Firewall

      sudo ufw allow Apache
      sudo ufw reload

##### 1.10. Create nagiosadmin User Account

      sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin

##### 1.10. Start Apache Web Server

      sudo systemctl restart apache2.service

##### 1.10. Start Service / Daemon

      sudo systemctl start nagios.service

##### 1.10. Launch nagios in brwoser at http://10.25.5.143/nagios

![image](https://user-images.githubusercontent.com/24622526/44909446-eb157700-ad0e-11e8-919d-68a357bc8244.png)


## Step-2: Install Plugins

##### 2.1. Install packages:

      sudo apt-get install -y autoconf gcc libc6 libmcrypt-dev make libssl-dev wget bc gawk dc build-essential snmp libnet-snmp-perl gettext

##### 1.10. Downloading The plugins

      cd /tmp
      wget --no-check-certificate -O nagios-plugins.tar.gz https://github.com/nagios-plugins/nagios-plugins/archive/release-2.2.1.tar.gz
      tar zxf nagios-plugins.tar.gz


##### 1.10. Compile + Install the plugins

      cd /tmp/nagios-plugins-release-2.2.1/
      sudo ./tools/setup
      sudo ./configure
      sudo make
      sudo make install
      
* http://10.25.5.143/nagios

* Wait for some time and launch the above URL in browser The error you previously saw should now disappear and the correct output will be shown on the screen.

##### 1.10.

##### 1.10. 


![image](https://user-images.githubusercontent.com/24622526/44909610-81499d00-ad0f-11e8-8c66-34ad9aa5428d.png)


sudo systemctl start nagios.service
sudo systemctl stop nagios.service
sudo systemctl restart nagios.service
sudo systemctl status nagios.service
