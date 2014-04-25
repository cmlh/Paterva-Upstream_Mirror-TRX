====================================================
NOTE: PLEASE READ TRX_DOCUMENTATION.PDF
No really - it's important.

You can find it on the Paterva.com website
in the documentation->developer->TDS section.
=====================================================






Prepping a server for use with the TDS (Python)
===============================================
We recommend using Ubuntu server with Apache2, Python 2.6, mod_wsgi and bottle. Assuming a stock standard Ubuntu server with Python installed the following is a recipe for building your environment:

Install Apache2
-------------------
sudo apt-get update
sudo apt-get install apache2

Install mod_wsgi
-------------------
sudo apt-get install libapache2-mod-wsgi

Install bottle
-------------------
sudo apt-get install python-setuptools
sudo easy_install bottle

Extract TRX files
------------------------
cd /tmp
tar -xvzf TRX_Ubuntu.tgz

Edit Apache configuration
-------------------------
Edit the file /etc/apache2/ports.conf and add the line:
Listen 9001
 
Add it just below the line that reads Listen 80 so the file looks like so:
…
NameVirtualHost *:80
Listen 80
Listen 9001
…

Copy the TRX Apache configuration file:
---------------------------------------
sudo cp /tmp/etc.apache2.sites-available/TRX /etc/apache2/sites-available/

Now enable the site:
-------------------
sudo a2ensite TRX

Install TRX files
-------------------
sudo mkdir /var/www/TRX
cd /var/www/TRX
sudo cp /tmp/var.www.TRX.tgz .
sudo tar -xvzf var.www.TRX.tgz

An example transform DNS2IP is provided (it’s a function defined in DNSTRANSFORMS.py, but more about that later). In the next section we will see how to configure the TDS to use this transform.

Restart Apache2
-------------------
sudo /etc/init.d/apache2 restart

Feel free to inspect the configuration of the ‘TRX’ site defined in /etc/apache2/sites-available and customize this to your liking. The configuration will route all traffic on port 9001 to the WSGI script TRX.wsgi located in /var/www/TRX.
