## Username and Password are great, but let's encrypt a ssh private key!

Let's update the `group_vars/all.yml` to look like:

```
- object: ssh-private-key
  content:
  - name: ssh-private-key
    template: "{{ inventory_dir }}/../templates/secrets/secret-ssh-private-key-template.yml"
    params_from_vars:
      SECRET_NAME: ricks-private-ssh-key
      SSH_PRIVATE_KEY: {{ ssh_private_key | b64encode }}
    namespace: "concentrated-dark-matter-secret\
    tags:
      - ssh-private-key
```{{copy}}

Notice the ` | b64encode }}` 

The ansible filter will encode it for us! No need to change your encrypted ssh-key! 

And we'll run it once more:
``ansible-playbook -i inventory/ apply.yml``{{execute}} 

