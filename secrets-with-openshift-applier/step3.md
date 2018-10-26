## Let's use ansible-vault to encrypt some things!

Ansible Vault is a command-line tool that allows you to encrypt (defaults to [AES256](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)) strings and files!

You can then assign them variable names and use them in your playbooks, they will be decrypted with a password that you create!

We're going to create a password file so that we don't have to pass in the password via command-line every time...

```
echo "f@k3Passw0rd1" >> ~/myPasswordFile.txt
```{{execute}}

Don't share this password! Please always abide by the "only verbally tell people" policy. Meaning we should never write it down on paper, or email it in plain text!

Next, we need to set a variable so Ansible knows what password to use to decrypt things...

```
export ANSIBLE_VAULT_PASSWORD_FILE=~/myPasswordFile.txt
```{{execute}}

