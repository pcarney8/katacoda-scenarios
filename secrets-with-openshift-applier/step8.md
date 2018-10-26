## Username and Password are great, but let's encrypt a ssh private key!
TODO: NEED TO CREATE A PRIVATE KEY HERE

First we need to create a private key

```
ssh-keygen -t rsa -b 4096 -C "computer@computer.com"
```{{execute}}

Just press enter through the prompts, if you need a refresher, go [here](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key)

Normally you would upload the public key (ends in `.pub`) into the hosted repository.

Now we just need to encrypt the private key!

Let's encrypt as a file this time:
```
cat ~/.ssh/id_rsa | base64 -w 0 | ansible-vault encrypt_string --stdin-name 'encrypted_private_key' >> encrypted-secrets.yml
```{{execute}}

Note ` | base64 -w 0 | ` in the middle, we are converting to base64 beforehand!

Have a look at the fully encrypted private key!
``cat encrypted-secrets.yml``{{execute}}

Add the template to the applier, and keep a variable there for the private key:
```
echo "- object: ssh-private-key
  content:
  - name: ssh-private-key
    template: \"{{ inventory_dir }}/../templates/secrets/secret-ssh-private-key-template.yml\"
    params_from_vars:
      SECRET_NAME: ricks-private-ssh-key
      SSH_PRIVATE_KEY: \"{{ encrypted_private_key }}\"
    namespace: \"concentrated-dark-matter-secret\"
    tags:
      - ssh-private-key" >> inventory/group_vars/all.yml
```{{execute}}

Let's go ahead and run it again:
``ansible-playbook -i inventory/ apply.yml``{{execute}}
