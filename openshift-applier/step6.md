####Before we can run this, we need to create a playbook which will call the OpenShift-Applier.

```
cat <<EOM >apply.yml
---
- name: Deploy {{ target }} 
    hosts: "{{ target }}"
    vars:
      ruby_namespace: "ruby-example"
    tasks:
      - include_role:
          name: openshift-applier/roles/openshift-applier
EOM
```{{execute}}

You can see this `{{ target }}` variable being called here. It's purpose is to allow you to run specific portions of the inventory if you want. 

Now we are ready to run!