# GCG_Odoo

**HOW TO HOST A FREE ODOO ERP ON GOOGLE CLOUD PLATFORM**
(without/with domain)  
---------------------------------------------------------------------------    
Based on:   
- "Setting up Odoo server on Ubuntu Google Cloud (2020)"  
https://www.youtube.com/watch?v=UAamkipG8R8  
  
- "INSTALACIÓN DE ODOO EN GOOGLE CLOUD"  
https://www.youtube.com/watch?v=S_QIHFpr37I  

- Odoo documentation   
https://www.odoo.com/documentation/14.0/setup/install.html#linux  

(But with few others steps)  
  
**The final project:**  
http://34.123.115.182:8069/  
.      
  
**1. CREATE A GOOGLE CLOUD PLATFORM ACCOUNT**  
First things first. Create yourself a Google Cloud Platform (GCP) account. This video will walk you through the process of setting up your GCP account if you don’t already have one  
  
**Info**: 
- https://youtu.be/XcjeGDeSEew   
  
    
**2. SPIN UP A COMPUTE ENGINE VM ON THE FREE TIER**  
From the GCP dashboard, click on Compute Engine. Create a VM instance.  
  
In order to create your VM instance on the free tier, you must configure your VM with the following restrictions:  
  
Non-preemptible f1-micro VM instance  
US regions: Oregon (us-west1), Iowa (us-central1), or South Carolina (us-east1)  
Up to 30 GB-months HDD  
  
![image](https://user-images.githubusercontent.com/72107370/109911977-234bf680-7c79-11eb-8d07-3b2a17ce30c5.png)
  
Notice how it says “Your first 744 hours of f1-micro instance usage are free this month”. This number will vary depending on how many days are in the current month. For example, this screenshot was from October which has 31 days.  

31 days x 24 hours = 744 hours (for month)  
Feel free to choose any operating systems for the boot disk. I chose Ubuntu 20.04 LTS.  

**Warning**:  
- It is necessary billing que VM engines, so you must add your bill acount, but with this configuration there will no cost for this website  
- Dont forget to check, Allow HTTP trafic and Allow HTTPs trafic on Firewall
  
  
**3. CONNECT YOUR DOMAIN NAME** (optional)  

You can optionally associate a domain name with your IP address. If you don’t have a domain name, feel free to skip ahead to the next step.  

Otherwise, you can use create a DNS A record at your domain registrar with a value of the IP address of your Google Cloud Platform VM instance.  

**Info**:   
It is possible purchase a domain for less than 3 o 12 $, I put a few web sites for buy a domain, if you want, but if you are watching this you don't need this :)    
- http://domain.google/  
- https://www.dreamhost.com/  
  
  
**4. LOGIN TO YOUR SERVER**  
  
Go to VM instance, go to connect in your intance they are differents option we go with.  
- Open in browser windows (it is a terminal of your computer in GCP)  
   
![image](https://user-images.githubusercontent.com/72107370/109912014-3f4f9800-7c79-11eb-8fdd-2a7df305ba36.png)
     
         
**5. UPDATE/UPGRADE YOUR VM**  

Once you’re logged in to your server, the first thing you want to do is update your system.  
  
- sudo apt update   
- sudo apt upgrade  
- sudo apt-get install nano   

**Info**:  
(Why? i like nano but you can install any tex editor, it will be necessary for configurated text files)  
[Fast commands: Ctrl o (save), Enter, Ctrl x] Also in this editor you can copy an paste text, cool no!  

  
**6. INSTALL THE WEB SERVER, DATABASE**, ...  
**PREPARE**  
Odoo needs a PostgreSQL server to run properly. The default configuration for the Odoo ‘deb’ package is to use the PostgreSQL server on the same host as your Odoo instance. Execute the following command in order to install the PostgreSQL server:  

- $ sudo apt install postgresql -y  

**Warning**  
wkhtmltopdf is not installed through pip and must be installed manually in version 0.12.5 for it to support headers and footers. So we did it ...
  
- sudo apt-get install wkhtmltopdf  
   
Test wkhtmltopdf  
- wkhtmltopdf https://www.google.ca/ google.pdf  
(the download file is in your home system)  
   
    
**INSTALL FROM REPOSITORY OR DEB PACKAGE**  
  Option 1 |OR|  Option 2  
  
**REPOSITORY** (Option 1)  
Odoo S.A. provides a repository that can be used with Debian and Ubuntu distributions. It can be used to install Odoo Community Edition by   executing the following commands as root:  
- wget -O - https://nightly.odoo.com/odoo.key | apt-key add -  
- echo "deb http://nightly.odoo.com/14.0/nightly/deb/ ./" >> /etc/apt/sources.list.d/odoo.list  
- apt-get update && apt-get install odoo  

You can then use the usual apt-get upgrade command to keep your installation up-to-date.  

At this moment, there is no nightly repository for the Enterprise Edition.  

**DEB PACKAGE** (Option 2)  
Instead of using the repository as described above, the ‘deb’ packages for both the Community and Enterprise editions can be downloaded from the official download page.  

Next, execute the following commands as root:  
- dpkg -i <path_to_installation_package> # this probably fails with missing dependencies  
- apt-get install -f # should install the missing dependencies  
- dpkg -i <path_to_installation_package>  

This will install Odoo as a service, create the necessary PostgreSQL user and automatically start the server.  
  
**Warning**  
The python3-xlwt and num2words does not exists in Debian Buster nor Ubuntu 18.04. If you need the feature, you can install it manually with:  
- sudo pip3 install xlwt  
-- sudo pip3 install num2words  

**7. EDIT FIREWALL SETTINGS**  
Go to   
Networking -> VPC network-> Firewall -> default-allow-internal  
Source filters -> IP ranges   
Add the range "0.0.0.0/0"  
  
Source filters -> Protocols and ports  
Change to "All"   
  
  
**LISTEN AND TEST**  

- sudo apt install net-tools  
- netstat -plntu  

The port 8069 it must be LISTEN  

Go to Compute Engine -> VM instances -> External IP (and clicked remenber put the port :8069 in the web browser)  

**8. INSTALL-SETUP ODOO**  

**Info:**  
When you clicked on the external IP aotomaticaly redirecto to a https, delete the s  
http://your-external-ip:8069  

        
**FIN**  
  
(They lived happily ever after ...)  

![image](https://user-images.githubusercontent.com/72107370/110049842-a83e1b00-7d20-11eb-8a49-2921156dca2e.png)

![image](https://user-images.githubusercontent.com/72107370/110049896-c0159f00-7d20-11eb-8338-28abab5fea32.png)


Example:  
http://34.123.115.182:8069
  
