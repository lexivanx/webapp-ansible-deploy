# Ansible Web App Deployment

This repository contains an Ansible playbook for configuring and deploying a web application to a group of servers. The playbook installs the required packages, configures the web server (Nginx), deploys the application code, and starts the required services.

## Prerequisites

- Ansible >= 2.9
- Python >= 3.5
- Target servers running Ubuntu 18.04 or later

## Getting Started

1. Clone this repository:

```
git clone git@github.com:lexivanx/webapp-ansible-deploy.git
```

2. Update the `inventory/hosts.ini` file with the correct server hostnames or IP addresses:

```
[web_servers]
web1.example.com
web2.example.com
```

3. (Optional) Customize the variables in `vars/main.yml` as needed:

```yaml
webapp_git_repo: https://github.com/yourusername/your-webapp-repo.git
webapp_service_name: your-webapp-service
```

4. (Optional) Update the `files/config.ini` with the correct settings for your application.

5. Run the Ansible playbook:

```
ansible-playbook -i inventory/hosts.ini webapp_deployment.yml
```

## Playbook Overview

The playbook includes the following tasks:

- Install required packages: Installs Python 3, Python 3 pip, and Nginx on the target servers.
- Configure Nginx: Deploys a templated Nginx configuration file for the web application.
- Enable webapp site: Creates a symlink to enable the Nginx site configuration.
- Deploy the application code: Clones the application Git repository to the target server's /var/www/webapp directory.
- Install application dependencies: Installs the application's Python dependencies using pip.
- Copy the configuration file: Copies the config.ini file from the files directory to the target server's /var/www/webapp directory.
- Start the required services: Starts and enables the Nginx and web application services.

## Directory Structure

- `inventory/`: Contains the inventory files for specifying target servers.
- `templates/`: Contains the `Jinja2` template files, including the Nginx configuration template.
- `files/`: Contains static files required by the playbook, such as the sample `config.ini`.
- `vars/`: Contains variable files, such as `main.yml`, for customizing playbook behavior.
