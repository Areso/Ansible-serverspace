# Ansible-serverspace
Ansible playbooks for infrastructure in Serverspace  

## Before you start
1. Get your API Key https://my.serverspace.ru/automation  
2. Create Ansible-vault file, for example `echo "AnsibleVaultPass" > ../ansible_vault.txt`  
3. `chmod 0640 ../ansible_vault.txt`
4. `ansible-vault encrypt_string --vault-password-file ../ansible_vault.txt 'yourapikey' --name 'xapikey'`  
where `yourapikey` is a variable value, you got in the first step  
insert this value into `group_vars/all.yml`

## Check, whether it's working
1. `ansible-playbook --vault-password-file ../ansible_vault.txt do_get_regions.yml` - you should get all regions  

## Create your first VM
1. 