# Ansible Odoo Deployment - Development in LXC container

## Usage

Feel free to change the example container name `odoo-12-dev`, shown in the examples.

### 1. Create and start container

`lxc launch <LXC_OS_IMAGE> <CONTAINER_NAME>`

**Example:**

`lxc launch ubuntu:18.04 odoo-12-dev`

### 2. Push SSH public key to container

```
lxc file push ~/.ssh/id_rsa.pub <CONTAINER_NAME>/root/.ssh/authorized_keys
lxc exec <CONTAINER_NAME> -- chown root: /root/.ssh/authorized_keys
lxc exec <CONTAINER_NAME> -- chmod 600 /root/.ssh/authorized_keys
```

**Example:**

```
lxc file push ~/.ssh/id_rsa.pub odoo-12-dev/root/.ssh/authorized_keys
lxc exec odoo-12-dev -- chown root: /root/.ssh/authorized_keys
lxc exec odoo-12-dev -- chmod 600 /root/.ssh/authorized_keys
```

### 3. Ansible deploy Odoo in LXC Container

Format:

`ansible-playbook -i <INVENTORY_FILE> <PLAYBOOK_FILE>`

For example:

`ansible-playbook -i local/12.0_development_lxc.inventory 12.0_development_lxc.yml`

### 4. Stop LXC Container

Required for the next steps.

`lxc stop <CONTAINER_NAME>`

**Example:**

`lxc stop odoo-12-dev`

### 5. User mapping host <=> container

`lxc config set <CONTAINER_NAME> raw.idmap 'both 1000 1000'`

**Example:**

`lxc config set odoo-12-dev raw.idmap 'both 1000 1000'`

### 6. Mount (some) host directory in path on the LXC Container

`lxc config device add <CONTAINER_NAME> homedir disk source=/home/<USER>/odoo/<PROJECT> path=/home/odoo/odoo`

**Example:**

`lxc config device add odoo-12-dev homedir disk source=/home/john/odoo/fancyparts path=/home/odoo/odoo`

### 7. Disable autostart of LXC Container

`lxc config set <CONTAINER_NAME> boot.autostart 0`

**Example:**

`lxc config set odoo-12-dev boot.autostart 0`

### 8. Start the LXC Container

`lxc start <CONTAINER_NAME>`

**Example:**

`lxc start odoo-12-dev`

## TODO

- Create (shell) script, which executes those commands, with container-name in arguments.

