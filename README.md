## Managed Node Requirements
- Ubuntu 16.04 64bit
- Install Python 2.7: `sudo apt install -y python2.7`
- Symlink `sudo ln -sf /usr/bin/python2.7 /usr/bin/python`

## Install ansible on control machine

    sudo apt-get install -y python2.7-dev python-pip
    sudo pip install --upgrade pip
    sudo pip install ansible

## Ansible Vault
We use vault to encrypt sensitive data stored in variables.
You have to provide password to decrypt data. Create **.vault_pass** file inside repository folder:

    echo 'vault_password' > .vault_pass

To view content of encrypted file run:

    ansible-vault view encrypted_file

To edit content of encrypted file run:

    ansible-vault edit encrypted_file

## Code style
- Use `command`/`shell` only if it's **extremly** necessary.
- Restart services only if it's **extremly** necessary.
- YAML code style example:

        - name: Configure MariaDB installation
          debconf:
            name: mariadb-server
            question: '{{ item }}'
            vtype: password
            value: '{{ db.root_password }}'
          with_items:
            - mysql-server/root_password
            - mysql-server/root_password_again
          changed_when: False

## Run ansible

On stage:

    ansible-playbook live.yml

## Smoke testing in Vagrant
You can use Vagrant to test ansible playbooks.

Up live environment:

    make live_up

Down any environment, e.g. live:

    make live_down

To see virtual machines:

    vagrant status

Ssh connect to virtual machine, e.g. live01:

    vagrant ssh live01

## Showroom users
- `ubuntu` Admin user.
- `drupal`. Project user.
- `www-data`. Nginx user

## Open ports
- 443
- 80 
- 22: for demo only
