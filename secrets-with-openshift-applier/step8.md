## Username and Password are great, but let's encrypt a ssh private key!

```
echo "- object: ssh-private-key
  content:
  - name: ssh-private-key
    template: \"{{ inventory_dir }}/../templates/secrets/secret-ssh-private-key-template.yml\"
    params_from_vars:
      SECRET_NAME: ricks-private-ssh-key
      SSH_PRIVATE_KEY: {{ ssh_private_key }}
    namespace: \"concentrated-dark-matter-secret\"
    tags:
      - ssh-private-key" >> inventory/group_vars/all.yml
```{{execute}}

Let's go ahead and run it again:
``ansible-playbook -i inventory/ apply.yml``{{execute}}

Fail! 

OpenShift needs things base64 encoded to pass them into the secret type: `kubernetes.io/ssh-auth`
