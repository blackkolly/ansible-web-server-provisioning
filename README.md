
# Web Server Provisioning with Ansible

This Ansible playbook automates the provisioning of a web server (Nginx or Apache) with all necessary configurations.

## Features

- Installs and configures Nginx or Apache web server
- Deploys a custom HTML page
- Creates a dedicated deployment user
- Optional Slack notifications
- Idempotent operations (safe to run multiple times)

## Prerequisites

- Ansible (>= 2.9.0)
- SSH access to target servers
- Ubuntu/Debian target servers (for apt package manager)
- For Slack notifications: Webhook URL

## Quick Start

1. Clone the repository:
   git clone https://github.com/yourusername/ansible-web-server-provisioning.git
   cd ansible-web-server-provisioning
       Create an inventory file (inventory.ini):

    [webservers]
    your_server_ip_or_hostname

    Create your custom index.html file or use the provided sample

    Run the playbook:

    ansible-playbook -i inventory.ini web_server_provisioning.yml

Configuration Options

Edit the variables in the playbook or use extra vars:
Variable	Default	Description
web_server	"nginx"	Web server to install ("nginx" or "apache")
html_file	"index.html"	Path to your HTML file
deployment_user	"deployer"	System user for deployments
slack_webhook_url	""	Slack webhook URL for notifications

Example with custom variables:

ansible-playbook -i inventory.ini web_server_provisioning.yml \
  -e "web_server=apache deployment_user=webadmin"

Slack Notifications

To enable Slack notifications:

    Create an Incoming Webhook in your Slack workspace

    Update the slack_webhook_url variable in the playbook

    Or pass it at runtime:

Verification

After running the playbook:

    Visit http://your_server_ip in a web browser

    Verify the deployment user:

    ssh deployer@your_server_ip

    Check service status:
   
    systemctl status nginx  # or apache2

## Structure

/ansible-web-server-provisioning
├── README.md
├── requirements.txt
├── web_server_provisioning.yml
├── index.html
└── inventory.ini.example


The `inventory.ini.example` would contain:

[webservers]
# Add your server IPs or hostnames here
# Example:
# 192.168.1.100
# myserver.example.com

This documentation provides clear instructions for users to get started with your playbook, explains all configuration options, and includes proper setup for the optional Slack notifications feature.
