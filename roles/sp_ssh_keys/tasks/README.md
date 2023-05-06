```
ansible-playbook --vault-password-file ../ansible_vault.txt  -e "operation=create ssh_key_name=fuego public_key='ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDPHverylongIHgsMC0ocK9S7GFQEuwBsZer1teo2vmMMuKRVryUWlB3hKOWCdmEUzutBd5Zaejnijn6Oz/Un8jCYFei1m/5nQtMHfGEaKj/6ggvcGQnsUqg3Hrz5vFDpFrxvhjoNrI7Pd/SdBSEPli3jreNX6DeZ88moRI fuego@laptop'" sp_ssh_keys.yml
```