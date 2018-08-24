Now we'll use the `openshift-applier` role to run the same `oc process` command, but piped into `oc apply`

Essentially: `oc process -f templates/app/ruby.yml --param-file params/ruby/build | oc apply -f -`

This is a powerful command that will ensure your template has all the necessary pieces in OpenShift

To get our current template to work with the `openshift-applier` we need to create the `openshift_cluster_content` to tell it to create OpenShift objects from the template and parameters.

You can learn more details about this [here](https://github.com/redhat-cop/openshift-applier/blob/master/roles/openshift-applier/README.md).

```
cat <<EOM >inventory/host_vars/application.yml
---
ansible_connection: local

openshift_cluster_content:
- object: ruby-components
    content:
    - name: ruby-ex
      template: "{{ playbook_dir }}/templates/app/ruby.yml"
      params: "{{ playbook_dir }}/params/ruby/build"
      namespace: "{{ ruby_namespace }}"
      tags:
      - app
EOM
```{{execute}}
