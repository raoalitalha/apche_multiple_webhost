# Hosting Multiple Websites on Apache Using Virtual Hosting

- In my last project, I hosted a single website on the [Apache server](https://github.com/raoalitalha/Apache-Website-Hosting.git). For details, please refer to the previous project documentation.
- In this current project, I will host two websites on a single machine using the Apache server.
- I am using the same OS on which I hosted my last project.

### **Purpose and Outcome**

The purpose of this project is to demonstrate the ability to configure an Apache server to host multiple websites on a single machine. This is a valuable skill in web development and server administration, allowing for efficient resource utilization and management. By the end of this project, you will have two fully functional websites hosted securely using HTTPS on a single Apache server instance.

# Step 1:

### Checking the System Configuration and Settings:

1. The user logged in as `root`

```bash
whoami   
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled.png)

1. The `current working dirrectory` is `/root`    

```bash
pwd
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%201.png)

1. The `hostname of the machine` is [`www.myproject.com`](http://www.myproject.com) . 

```bash
hostname
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%202.png)

- We will change the `hostname` to `www.myproject2.com`

```bash
 hostnamectl set-hostname www.myproject2.com
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%203.png)

1. The the information about the `current OS relase and version`  can be viewed using the command :

```bash
cat /etc/os-release
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%204.png)

- To check just the `Red Hat release name and version`:

```bash
cat /etc/os-release

```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%205.png)

- The `kernal information` , `pc architecture` and other information can be viewed using :

```bash
hostnamectl
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%206.png)

1. As a good practice `checking any update` for the `current OS`

```bash
dnf check-update
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%207.png)

- Minor updates are available. Apply the updates

```bash
dnf update -y
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%208.png)

1. Checking the `ip address` of the machine:

```bash
ip add
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%209.png)

- To narrow down the ip address :

```bash
ip a | grep enp0s3
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2010.png)

- The `ip address` of the current machine is `192.168.1.15`

# Step 2:

## Checking The Necessary `packages`  . Downloading new `packages`. Inspecting the `directories`

1. Now, we need some packages to deploy `two websites servers` on our single machine.

### Package 1 , Apache HTTP:

1. We need to download and install the `apache server` `httpd` on our machine. 
2. Checking the `repositories` if it is already installed or not:

```bash
rpm -qa | grep httpd
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2011.png)

- Turned out `httpd` already installed in my machine. Let’s check for any update available for the package

```bash
dnf update httpd*
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2012.png)

- My `apache server` package is Updated to current version.
1. I can view my the directory of `httpd`  at `cd /var/www/html`

```bash
cd /var/www/html/

ls -ltr
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2013.png)

1. Files from my `previous project website` is still here. I want to deploy new websites . So lets remove it. I am currently in directory `/var/www/html` . Run the command :

```bash
rm -rf ./*
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2014.png)

- All the files has been deleted from the directory.

### Package 2 and 3 , `opensll` and `mod_ssl`:

1. For this project we are deploying two website on with `enable secure communication` in short `https`. 
2. We need `SSL/TLS certificate` to use `https`
3. To achieve this we need to install two packages `openssl` and `mod_ssl`. They form `secure connection` between `web server` and `user browser`.
4. They both packages work together for `encryption` and `decryption`
5. We will create `certificate` using the package `openssl` while `mod_ssl` is a supportive package for `openssl`
6. First, check either the both packages are installed in our current system or not. Checking the `openssl` first and if installed updating it.

```bash
rpm -qa | grep openssl

```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2015.png)

 -  

- The package `openssl` is already installed. Let’s check updates:

```bash
	dnf update openssl
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2016.png)

- The package is updated already.
1. Checking the package `mod_ssl` . Installing if needed .

```bash
rpm -qa | grep mod_ssl
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2017.png)

- The package is not installed on my machine. Let’s install it:

```bash
dnf install mod_ssl
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2018.png)

# Step 3:

## Creating `self signed Certificate` Using `OpenSSL`

1. We have installed the package `openssl` and `mod_ssl`. Now , we will create `SSL/TLS` certificate.
2. Here we will call it `SAN` certificate `(Subject Alternative Names)` instead of `SSL/TLS` certificate `(Secure Sockets Layer/Transport Layer Security)` . Basically both are same , but with one difference in nature:
    1. SSL/TLS : This certificate is used to deploy one `single domain` on `one certificate only`
    2. SAN : This certificate is used to deploy `multiple domain names` in a `single certificate`
3. To `install and configure` the certificate use the command :

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout localhost.key -out localhost.crt

- openssl req = Requesting for Certificate
- -x509   =  Creates a self-signed certificate instead of a certificate signing request (CSR)
- `-nodes`: Omits private key encryption. **Note:** This is not recommended for production environments as it stores the private key unencrypted.
- `-days 365`: Sets the certificate validity period to 365 days (one year).
- `-newkey rsa:2048`: Generates a new RSA private key with a size of 2048 bits. This key will be used for encryption and decryption by your server.
- `-keyout localhost.key`: Specifies the filename for the private key (localhost.key in this case)
- `-out localhost.crt`: Specifies the filename for the generated certificate (localhost.crt in this case)
```

- Explanation of the command is :
    - openssl req = Requesting for Certificate
    - -x509   =  Creates a self-signed certificate instead of a certificate signing request (CSR)
    - `-nodes`: Omits private key encryption. **Note:** This is not recommended for production environments as it stores the private key unencrypted.
    - `-days 365`: Sets the certificate validity period to 365 days (one year).
    - `-newkey rsa:2048`: Generates a new RSA private key with a size of 2048 bits. This key will be used for encryption and decryption by your server.
    - `-keyout localhost.key`: Specifies the filename for the private key (localhost.key in this case)
    - `-out localhost.crt`: Specifies the filename for the generated certificate (localhost.crt in this case)
    
    ![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2019.png)
    
    ![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2020.png)
    
    - You will be prompt for some information which you have to fill to obtain certificate.

> If you have put wrong information and want to change it itis not recommended. Best practice is to create a new certificate.
> 

# Step 4

## Copying the certificate generated files to proper destination

1. While we were `generating our `SAN certifictae`. We were in the directory name `/var/www/html` . 

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2021.png)

1. We will move the two generated files named `localhost.key` and `localhost.crt`  to the directory `/root`. It is good to have a copy of  keys.

```bash
mv localhost.key localhost.crt /root
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2022.png)

1. We have to move the generated files to specific directories:
    1. `localhost.key`  copy to `/etc/pki/tls/private/`
    2. `localhost.cert` copy to `/etc/pki/tls/cert/`

1. Before we move them we have to do two things:
    1. The directories are presnt
    2. We have to check the file named `ssl.conf` present in directory `cat /etc/httpd/conf.d/ssl.conf` that the path were we copying the file `localhost.key` and `localhost.cert` are mention exactly the same way ``/etc/pki/tls/private/` and `/etc/pki/tls/cert/`
    
    ![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2023.png)
    

1. Now we will move the file name `localhost.key` to the directory `/etc/pki/tls/private/`

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2024.png)

1. The filename `localhost.crt` will be moved to the directory `/etc/pki/tls/cert/`

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2025.png)

1. Now to verify that the syantax of the configuration files is okay or not. Run the command:
    
    ```bash
    httpd -t
    ```
    
    ![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2026.png)
    
- Since its shows the message `Sytanx OK` so everything is working perfectly.
- Sometime if there is any error, read the display message there could be a minor issue, like spelling mistake, spelling mismatch, wrong server name , or any colon or semi-colon error.

# Step 5:

1. As we know we want to deploy two websites on our machine. For this reason we have to create two directories in the `/var/www/html
2. We will create two directories with name `website1` and `website2` . Where we will place our `website code.`.
3. Let’s create the directory name `website1` in `/var/www/html/` and download the website code using `wget [https://www.free-css.com/assets/files/free-css-templates/download/page284/mical.zip](https://www.free-css.com/assets/files/free-css-templates/download/page284/mical.zip)` .Then unzip it and remove the unnessary zipped file afterward.

```bash
cd /var/www/html/
 
mkdir website1

cd website1

wget [https://www.free-css.com/assets/files/free-css-templates/download/page284/mical.zip](https://www.free-css.com/assets/files/free-css-templates/download/page284/mical.zip)
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2027.png)

- The website `zip` file is downloaded:

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2028.png)

- Unzip the file using the command:

```bash
unzip Mical Free Website Template - Free-CSS.com.zip
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2029.png)

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2030.png)

- Remove the downloaded zip file as we do not need it anymore.

```bash
rm -r Mical\ Free\ Website\ Template\ -\ Free-CSS.com.zip

```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2031.png)

- Open the directory `cd mical-html/` and copy the whole content to the directory `website1` and  afterward remove the directory `mical-html

```bash
#Enter in directory `mical-html/`
cd mical-html/

# Copy the enitire content to the parent directory whischis `var/www/html/website1
cp -r * ..

#Now remove the extra folder which is `mical-html/
rm -rf mical-html
```

## Repeat the same procedure for the second website

1. As we know we want to deploy two websites on our machine. For this reason we have to create two directories in the `/var/www/html
2. We will create two directories with name `website1` and `website2` . Where we will place our `website code.`.
3. Let’s create the directory name `website2` in `/var/www/html/` and download the website code using `wget [https://www.free-css.com/assets/files/free-css-templates/download/page284/pet-shop.zip](https://www.free-css.com/assets/files/free-css-templates/download/page284/pet-shop.zip)` .Then unzip it and remove the unnecessary zipped file afterward.

```bash
cd /var/www/html/
 
mkdir website2

cd website1

wget [https://www.free-css.com/assets/files/free-css-templates/download/page284/pet-shop.zip](https://www.free-css.com/assets/files/free-css-templates/download/page284/pet-shop.zip)
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2032.png)

1. The website `zip` file is downloaded as `pet-shop.zip`
2. Unzip the file using the command:

```bash
unzip pet-shop.zip
```

1. After unzipping remove the file `pet-shop.zip`

```bash
	rm -rf pet-shop.zip
```

1. Copy the entire content to the parent directory which is `var/www/html/website2`

```bash
cp -r * ..
```

1. Remove the extra directory

```bash
rm -rf pet-shop-website-template/

```

# Step 6:

## Creating Virtual Host , For Hosting two website on single Machine.

1. To make it possible that we will host two website . We have to use the concept of `virtual hosting`. In which we will create two file named `website1.conf` and `website2.conf` in the directory `cd /etc/httpd/conf.d` 

```bash
touch website1.conf website2.conf
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2033.png)

1. Using the `vi editor` we will do some configuration in both files. Open the file `website1.conf` The configuration in the file name `website1.conf` will be :

```bash
<VirtualHost *:443>  # Defines a virtual host for incoming connections on all interfaces (*) using port 443 (standard HTTPS port).
  SSLEngine on        # Enables the SSL engine for this virtual host, necessary for secure connections.
  SSLCertificateFile /etc/pki/tls/certs/localhost.crt  # Path to the SSL certificate file for the website.
  SSLCertificateKeyFile /etc/pki/tls/private/localhost.key  # Path to the private key file associated with the SSL certificate.
  ServerName www.carrepairing.id  # Specifies the server name that this virtual host will respond to (your website domain).
  DocumentRoot /var/www/html/website1  # The directory where Apache will look for website files when a request is received for www.carrepairing.id.
</VirtualHost>

```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2034.png)

1. Open the file `website2.conf` The configuration in the file name `website1.conf` will be :

```bash
<VirtualHost *:443>
SSLEngine on
SSLCertificateFile /etc/pki/tls/certs/localhost.crt
SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
ServerName www.petshop.id
DocumentRoot /var/www/html/website2
</VirtualHost>
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2035.png)

# Step 7:

1. We have configured the directory, our website code is in their respective directory already.
2. In this step we will go to the directory `vim /etc/hosts` and define the `ip address` and `domain names`
3. Our `ip address` is `192.168.1.15` 
4. The domain names are [`www.carrepairing.id`](http://www.carrepairing.id) and `www.petshop.id`
5. Open the file in vim editor:

```bash
vim /etc/hosts
```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2036.png)

1. Add the following details:

```bash
192.168.1.15 www.carrepairing.id
192.168.1.15 www.petshop.id

```

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2037.png)

1. Save the file

# Step 8:

## Restart HTTPD service and Firewall setting:

- It is always a good practice to restart the `apache server` so run the following commands:

```bash
systemctl reset-failed httpd.service

systemctl start httpd.service

systemctl status httpd.service

```

- **Firewall Configuration:** Ensure your firewall is configured correctly to allow HTTP and HTTPS traffic. So run these command one by one

```bash
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload
```

# Step 9:

## Testing the website

- In your local machine open your web browser and enter url [`www.carrepairing.id`](http://www.carrepairing.id) and `www.petshop.id`

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2038.png)

![Untitled](Hosting%20Multiple%20Websites%20on%20Apache%20Using%20Virtual%20%207bdaff0c3b9b4fafb644b6c4be82518d/Untitled%2039.png)

# **Conclusion**

By following these steps, you will successfully host two websites on a single Apache server. This setup is efficient and demonstrates important skills in server configuration, virtual hosting, and secure communication using SSL/TLS.