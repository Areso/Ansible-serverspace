# Ansible-serverspace
Ansible playbooks for an infrastructure in Serverspace  

## Before you start
1. Get your API Key https://my.serverspace.ru/automation  
2. Create Ansible-vault file, for example `echo "AnsibleVaultPass" > ../ansible_vault.txt`  
3. `chmod 0640 ../ansible_vault.txt`
4. `ansible-vault encrypt_string --vault-password-file ../ansible_vault.txt 'yourapikey' --name 'xapikey'`  
where `yourapikey` is a variable value, you got in the first step  
insert the output to `group_vars/all.yml`  
  
## OPTIONALLY:  
if you wanna not only create VMs and install software, but also register their names with DNS, then you need to peform a bit more:  
5. Register a domain  
6. Transfer DNS of the domain to Cloudflare  
7. Create your API Token (in open your profile in the top-right icon->My Profile)  
8. Open site, get from bottom-right Zone ID
9. Encrypt your API Token:  
`ansible-vault encrypt_string --vault-password-file ../ansible_vault.txt 'yourCloudlareAPITokne' --name 'clfr_auth_key'`
10. Encrypt your email:
`ansible-vault encrypt_string --vault-password-file ../ansible_vault.txt 'yourCloudflareEmail' --name 'clfr_auth_email'`
11. Encrypt your Zone ID:
`ansible-vault encrypt_string --vault-password-file ../ansible_vault.txt 'yourZoneId' --name 'clfr_zone_id'`
12. Now you can check whether it's working for you:
`ansible-playbook --vault-password-file ../ansible_vault.txt clfl_get_dns_records.yml`

  
## Working with references: acquring public information
1. `ansible-playbook --vault-password-file ../ansible_vault.txt sp_get_locations.yml` - get locations, and their options  
2. `ansible-playbook --vault-password-file ../ansible_vault.txt sp_get_images.yml`    - get images, and their options  
## Working with user-related data:
1. `ansible-playbook --vault-password-file ../ansible_vault.txt sp_get_project.yml`   - get user's project (binded to the API token), balance   
2. `ansible-playbook --vault-password-file ../ansible_vault.txt sp_ssh_keys.yml`      - get user's ssh keys  
3. `ansible-playbook --vault-password-file ../ansible_vault.txt  -e "operation=create ssh_key_name=fuego public_key='ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDPHverylongIHgsMC0ocK9S7GFQEuwBsZer1teMuKRVryUWlB3hKOWCdmEUzutBd5Zaejnijn6Oz/Un8jCYFei1m/5nQtMHfGEaKj/6ggvcGQnsUqg3Hrz5vFDpFrxvhjoNrI7Pd/SdBSEPli3jreNX6DeZ88moRI fuego@laptop'" sp_ssh_keys.yml` - add ssh publick key to the user    
4. `ansible-playbook --vault-password-file ../ansible_vault.txt -e "operation=get_by_id ssh_key_id=8322" sp_ssh_keys.yml` - get user ssh key by id  
5. `ansible-playbook --vault-password-file ../ansible_vault.txt -e "operation=delete ssh_key_id=11340" sp_ssh_keys.yml` - delete user key by key id  
##  
  
## Create your first VM
1. `ansible-playbook --vault-password-file ../ansible_vault.txt sp_get_servers.yml` - get all your servers  
--for whom who may concern: it asks sudo password to add records to /etc/hosts--  
--rols/sp_vm_create/tasks/main.yml # add_host_to_hosts task--  
2. `ansible-playbook --vault-password-file ../ansible_vault.txt -i "test1, " -K sp_vm_create.yml` - create vm called `test1`  
3. `ansible-playbook --vault-password-file ../ansible_vault.txt -i "test46, " -e "image='{{ images.ub2204 }}'" -K sp_vm_create.yml` -- create VM with non-default OS (Ubuntu 20.04 is default)  
4. `ansible-playbook --vault-password-file ../ansible_vault.txt -i "test46, " -e "image='{{ images.windows19 }}'" -K sp_vm_create.yml` 
5. `ansible-playbook --vault-password-file ../ansible_vault.txt -i "test1, " -e "dns=cloudflare" sp_vm_create.yml` - create vm called `test1` with using cloudflare DNS, after creation it would be accessible as `test1.xlaba.site`
