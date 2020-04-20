## VM Setup
### SSH Access - depman.sigint.cse

To give ssh access to depman for the vm add the appropriate account authorization keys to the service account.
The account authorization files can be found in this projects `./resources/etc/ssh/accounts/[service account]/` folder.
They `authorized_keys` file should be placed in the VM's `/etc/ssh/accounts/[service account]/` directory.
Permissions of the directory needs to be set to 711.
Permissions of the file `authorized_keys` needs to be set to 744.

Update `/etc/security/access.conf` on the remote server to allow the deployment manager access to connect to the VM

### BOB VM Setup
`+ : @builder-ng : ALL`

`+ : sa-bob : ALL`

### MQ VM Setup
`+ : @mq-ng : ALL`

`+ : sa-mq : ALL`

##Common

### Root Access - depman.sigint.cse

Add the appropriate account access to a root shell in order for ansible to make changes on the VM.
The account access files can be found in this projects `./resources/etc/sudoers.d/` folder.
They should be placed in the VM's `/etc/sudoers.d/` directory.
Permissions of the directory needs to be set to 440.
Permissions of the file needs to be set to 440.
Permissions need to be set to 640.



### Queue Manager - BlockIP

The queue managers require an update to allow the hlt vm's permission to connect to the hlt queue managers.
Refer to the config files located in `./resources/var/mqm/exist/BlockIP.ini_[host]` when updated the configs in
the folder `/var/mqm/exits/BlockIP.ini`

## Ansible Execution
### Galaxy Dependencies
```
ansible-galaxy remove ~/.ansible/roles/*

ansible-galaxy install -r requirements.yml
```

### Running Ansible
```
ansible-playbook -i inventory/staging provision_hlt.yml
```