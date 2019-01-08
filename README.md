# Ansible-Postfix-GSuite-Relay
Basic Ansible script to configure postfix to relay via GSuite.

Script configures postfix to relay via a central Gsuite account enabling users to take advantage of SPF/DKIM/DMARC without managing those records directly.  If you have a lot of machines, you likely want to run this on a 'relay' node instead of all machines, and have all the machines setup to relay through the relay node.  Yes, relay to a relay to a relay.

Requirements: 
 * Ubuntu 18 / Debian 9
 * Python 3

### Setup python virtual environment for consistent ansible environment
```
python -m venv ~/.ansible
source ~/.ansible/bin/activate

pip install --upgrade pip
pip install ansible==2.7.4
```

### Clone ansible-zabbix repo
```
git clone https://github.com/Revenni/Ansible-Postfix-GSuite-Relay.git
```
### Edit inventory file, at minimum change the IP.
Remote user defaults to root via inventory.  Playbook does use become, so if you connect via a different user feel free to change the user specified in inventory.

```
vi ansible/inventory
```

### Edit postfix/sasl/sasl_passwd to contain the proper credentials
Leave smtp.gmail.com there, just update the username:password pair.
```
smtp.gmail.com username@domain.com:password
```

### Run playbook
ansible-playbook -i ansible/inventory main.yml
