# Ansible AWS Webserver Project

This project configures the 3 EC2 hosts in the `aws` inventory group using Ansible.

## What the playbook does

- Installs and starts `firewalld`
- Opens ports `80` and `443` from group variable `ports` in `starter/group_vars/aws.yml`
- Checks `/var/www/html/www.companyplus.com` and prints status with `debug`
- Runs `webserver` role to:
  - install `nginx` using role var `webserver`
  - create site directories with `nginx:nginx` and mode `0770`
  - template `nginx.conf` using `app_root`, `server_name`, and `document_root`
  - restart `nginx` via handler

## Run

From the `starter` directory:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

Playbook passes role vars:
- `app_root: html_demo_site-main`
- `server_name: "{{ ansible_default_ipv4.address }}"`
- `document_root: /var/www/html`

## License

[LICENSE.txt](LICENSE.txt)
