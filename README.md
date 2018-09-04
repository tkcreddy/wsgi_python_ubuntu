# wsgi_python_ubuntu

Introduction

mod_wsgi is an Apache module that provides a standard and efficient method for dynamic web applications to communicate with Apache web servers. mod_wsgi is a simple to use module that can be used to host any Python web application which supports the Python WSGI specification. It is used to deploy applications written with different tools such as Django, TurboGears, and Flask.

In this tutorial, we will demonstrate the installation and set up of mod_wsgi with the Apache web server on Ubuntu

Getting Started

Let's start making sure that your Ubuntu server is fully up to date. You can update your server by running the following command:

sudo apt-get update -y
sudo apt-get upgrade -y


Installing mod_wsgi

Before starting, you will need to install some prerequisite Apache components in order to work with mod_wsgi. You can install all required components by simply running the following command:

sudo apt-get install apache2 apache2-utils libexpat1 ssl-cert python

Once all of the Apache components have installed, use the curl command to verify the Apache server is responding.

curl http://localhost

You should see the default Ubuntu Apache page.

Now, install mod_wsgi by running the following command:

sudo apt-get install libapache2-mod-wsgi
Restart Apache service to get mod_wsgi to work.

sudo /etc/init.d/apache2 restart

Creating WSGI website
To serve the python application, it is important that Apache forward certain types of requests to mod_wsgi. It is also important to create a python file that tells mod_wsgi how to handle these requests.

You can do this by creating a website for WSGI that will tell Apache the location of python file and setup the file accordingly.

sudo nano /etc/apache2/conf-available/wsgi.conf
Add the following line:

WSGIScriptAlias /test_wsgi /var/www/html/test_wsgi.py
Next, create a python test script which you set above.

sudo nano  /var/www/html/test_wsgi.py
Add the following line:

def application(environ,start_response):
    status = '200 OK'
    html = '<html>\n' \
           '<body>\n' \
           '<div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">\n' \
           'mod_wsgi Test Page\n' \
           '</div>\n' \
           '</body>\n' \
           '</html>\n'
    response_header = [('Content-type','text/html')]
    start_response(status,response_header)
    return [html]


When you are finished save and close the file.

Once you are done with it, you will need to enable the WSGI configuration and restart Apache.

sudo a2enconf wsgi

sudo /etc/init.d/apache2 restart


