# Ansible Odoo Deployment

Example playbooks and guide for the Ansible Odoo role.

- Check the different kind of setups or provisioners.
- Contribution (PR or issue) is highly appreciated.


## Create your ansible-odoo-deploy (Git) project

Either:

1. Create such a **ansible-odoo-deploy** repository for your project and create or copy example file(s).

... OR ...

2. Import (copy) this repository to your Git environment and copy example file(s).

## Server

Root access is the quickest and easiest (not safest) way to deploy.\
Ensure your SSH public-key (e.g. from `~/.ssh/authorized_keys` file) is copied into `/root/.ssh/authorized_keys`.

## Local

**On your local desktop, development machine.**

**Install Ansible**

```
pip3 install ansible
cd ~/.ansible/roles
```

Either:

1. Clone the upstream **ansible-odoo** project:\
`git clone https://github.com/OCA/ansible-odoo`

 ... OR ...

2. Clone my **ansible-odoo** fork, which has some new features merged from PR's:\
`git clone https://github.com/novacode-nl/ansible-odoo`

Ensure you have access to the **ansible-odoo-deploy** repository (e.g. by your SSH public key).

Git clone the project its **ansible-odoo-deploy** repository.

In the **ansible-odoo-deploy** directory, you basically need 2 files (which you can give any name):

- A "`playbook.yml`" (such files as in the example directories).
- An Ansible "`inventory`" (INI, or Yaml) file, which configures your hosts used in the playbook file.

Commit and push the changes to **ansible-odoo-deploy** repository.

Run the deployment with the`ansible-playbook` command.

Format:

`ansible-playbook -i <INVENTORY_FILE> <PLAYBOOK_FILE>`

For example:

`ansible-playbook -i odoo-12.0-staging.inventory odoo-12.0-staging.yml`
