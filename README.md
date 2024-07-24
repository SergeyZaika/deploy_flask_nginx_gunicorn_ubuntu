# Ansible Playbooks for Setting Up and Tearing Down Nginx, Gunicorn, and Flask on Ubuntu 20.04

This repository contains two Ansible playbooks:
1. `setup_nginx_gunicorn_flask.yml`: A playbook to set up Nginx, Gunicorn, and Flask on an Ubuntu server.
2. `remove_nginx_gunicorn_flask.yml`: A playbook to remove the Nginx, Gunicorn, and Flask setup from the server.

## Requirements

- Ansible installed on your local machine.
- A remote Ubuntu server with SSH access.
- Ports 22, 80, and 443 open on the remote server.

## Usage

### Setup Playbook

1. Clone the repository:
    ```sh
    git clone https://github.com/your_username/your_repository.git
    cd your_repository
    ```

2. Update the `hosts` file with your server details.

3. Update the variables in the `setup_nginx_gunicorn_flask.yml` file as needed:
    - `user`: The username to use for SSH.
    - `project_name`: The name of your project.
    - `domain_name`: The domain name for your server.

4. If you do not want to install SSL certificates using Certbot, comment out the lines related to obtaining SSL certificates in the `setup_nginx_gunicorn_flask.yml` file:
    ```yaml
    # - name: Obtain Let's Encrypt SSL certificate
    #   command: certbot --nginx -d {{ domain_name }}
    #   args:
    #     creates: /etc/letsencrypt/live/{{ domain_name }}/fullchain.pem
    ```

5. Run the setup playbook:
    ```sh
    ansible-playbook setup_nginx_gunicorn_flask.yml -i hosts
    ```

### Remove Playbook

1. Ensure the variables in the `remove_nginx_gunicorn_flask.yml` file match those used in the setup playbook.

2. Run the remove playbook:
    ```sh
    ansible-playbook remove_nginx_gunicorn_flask.yml -i hosts
    ```

## Files

- `setup_nginx_gunicorn_flask.yml`: Playbook to set up Nginx, Gunicorn, and Flask.
- `remove_nginx_gunicorn_flask.yml`: Playbook to remove the Nginx, Gunicorn, and Flask setup.
- `templates/app.py.j2`: Jinja2 template for the Flask application.
- `templates/gunicorn.service.j2`: Jinja2 template for the Gunicorn service.
- `templates/nginx.conf.j2`: Jinja2 template for the Nginx configuration.
- `hosts`: Ansible inventory file to define your servers.