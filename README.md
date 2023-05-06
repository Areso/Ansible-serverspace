# Ansible-serverspace
Ansible playbooks for an infrastructure in Serverspace  

## Before you start
1. Get your API Key https://my.serverspace.ru/automation  
2. Create Ansible-vault file, for example `echo "AnsibleVaultPass" > ../ansible_vault.txt`  
3. `chmod 0640 ../ansible_vault.txt`
4. `ansible-vault encrypt_string --vault-password-file ../ansible_vault.txt 'yourapikey' --name 'xapikey'`  
where `yourapikey` is a variable value, you got in the first step  
insert the output to `group_vars/all.yml`  
  
OPTIONALLY:  
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

  
## Check, whether it's working
1. `ansible-playbook --vault-password-file ../ansible_vault.txt sp_get_locations.yml` - you should get all regions  
2. `ansible-playbook --vault-password-file ../ansible_vault.txt sp_get_images.yml`    - you should get images  
3. 

## Create your first VM
1. 