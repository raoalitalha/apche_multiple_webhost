# Advanced Apache Hosting with SSL: Multi-Website Configuration

This project demonstrates the process of hosting two separate websites on a single Apache server. It includes configuring virtual hosts, setting up SSL/TLS for secure communication, and managing multiple websites efficiently.

This project is a continuation of my last project, [Apache-Website-Hosting](https://github.com/raoalitalha/Apache-Website-Hosting.git), where I initially set up a single website on an Apache server. Now, I have expanded it to host multiple websites with secure HTTPS connections.

## Project Overview

This project aims to:

- Configure an Apache server to host multiple websites.
- Set up secure HTTPS connections using self-signed SSL certificates.
- Utilize virtual hosts to manage different websites on a single server.

## Prerequisites

- A machine running a Red Hat-based OS (e.g., CentOS, Fedora).
- Basic knowledge of Linux command-line operations.
- Apache HTTP Server installed.

## Steps to Achieve the Project

### 1. Checking System Configuration

Ensure you are logged in as the root user and verify the current system settings.

### 2. Installing Necessary Packages

Install and update Apache, OpenSSL, and mod_ssl.

### 3. Creating a Self-Signed Certificate

Generate a self-signed SSL certificate to secure your websites.

### 4. Setting Up Directory Structure

Create directories for your websites and download website templates.

### 5. Configuring Virtual Hosts

Set up virtual host configuration files to manage multiple websites.

### 6. Defining IP Address and Domain Names

Update the /etc/hosts file to map your domains to your IP address.

### 7. Restarting Services and Configuring Firewall

Restart the Apache server and configure the firewall to allow HTTP and HTTPS traffic.

### 8. Testing the Websites

Verify that both websites are accessible via the configured domain names.

## Conclusion


This project demonstrates how to efficiently host multiple websites on a single Apache server using virtual hosts and secure them with SSL/TLS. This skill is essential for web developers and system administrators, highlighting your ability to manage web server configurations effectively.

## Future Plans
In the future, I plan to:

Deploy the Websites on an Nginx Server in Linux: Transition from Apache to Nginx for better performance and resource management.
Automate Deployment: Use tools like Ansible or Puppet to automate the deployment process.
Implement Continuous Integration/Continuous Deployment (CI/CD): Integrate with CI/CD pipelines to streamline updates and maintenance.


