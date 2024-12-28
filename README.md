# lab5
## How to start the lab
1. Create SSH keypair
2. Create file `./vagrant-config.rb` with variables:
```
$BRIDGE = "<your_bridge_interface>"
$SSH_PUBLIC_KEY_PATH = "<path_to_your_public_ssh_key>"
```
3. `vagrant up`
4. Wait lol
5. ansible-playbook -i ./inventories/demo/hosts playbook.yml --ask-vault-password
6. Wait lol 2
7. Ready!
