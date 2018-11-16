## Let's quickly setup everything to run the applier with the secrets!

First the `hosts` file:

```
cat <<EOM >inventory/hosts
[seed-hosts]
localhost ansible_connection=local
EOM
```{{execute}}


and the playbook just like last time:

```
cat <<EOM >apply.yml
---
- name: Create Project and Secret Example 
  hosts: "seed-hosts"
  tasks:
    - include_vars: "{{ inventory_dir }}/../encrypted-secrets.yml"
    - include_role:
        name: openshift-applier/roles/openshift-applier
EOM
```{{execute}} 

Notice that we're adding a task here! `include_vars` will include the encrypted username and password that we created!

We'll pull in the `openshift-applier` role using `ansible-galaxy`!
```
cat <<EOM >requirements.yml
- name: openshift-applier
  scm: git
  src: https://github.com/redhat-cop/openshift-applier
  version: v2.0.3
EOM
```{{execute}}

And now let's run the galaxy command:
``ansible-galaxy install -r requirements.yml -p roles``{{execute}}

Finally, let's run it!
``ansible-playbook -i inventory/ apply.yml``{{execute}}

Fail! 

OpenShift needs things base64 encoded to pass them into the secrets of type: `Opaque`

NOTE: if you need a refresher on what we're doing in this step, please refer to [here](https://katacoda.com/patrickcarney/scenarios/openshift-applier)

