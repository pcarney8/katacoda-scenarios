## Inventory Setup

We'll set up our `openshift_cluster_content` variable first:
```
cat <<EOM >inventory/group_vars/all.yml
---
ansible_connection: local

openshift_cluster_content:
- object: secrets
  content:
  - name: user-pass
    template: "{{ inventory_dir }}/../templates/secrets/secret-user-pass-template.yml"
    params_from_vars: 
      SECRET_NAME: user-pass
      USERNAME: "{{ encrypted_username }}"
      PASSWORD: "{{ encrypted_password }}"
    action: create
    ignore_unknown_parameters: false
    namespace: concentrated-dark-matter-secret
    tags:
      - secrets
      - secrets-user-pass
EOM
```{{execute}}

Notice the `encrypted_username` and `encrypted_password` variables!

Ansible will automatically decrypt these variables when we run the applier and put them into the template!

Since we aren't creating a project with the applier in this inventory, let's go ahead and manually create one:

```
oc new-project concentrated-dark-matter-secret
```{{execute}}
