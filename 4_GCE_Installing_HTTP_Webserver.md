# Installing HTTP Webserver on Google Compute Engine Virtual Machine

## Overview

Google Compute Engine (GCE) virtual machines can be configured to serve web content by installing an HTTP web server. Apache is a widely used server for this purpose, providing a reliable platform for hosting websites and web applications.

---

## Steps

### 1. Connect to the VM

Access the VM instance via SSH using the GCP Console or `gcloud` CLI. Ensure pop-ups are enabled if connecting through the web interface.

### 2. Obtain Root Privileges

Administrative access is required to install software:

```bash
sudo su
sudo su
apt update 
apt install apache2
ls /var/www/html
echo "Hello World!"
echo "Hello World!" > /var/www/html/index.html
echo $(hostname)
echo $(hostname -i)
echo "Hello World from $(hostname)"
echo "Hello World from $(hostname) $(hostname -i)"
echo "Hello world from $(hostname) $(hostname -i)" > /var/www/html/index.html
