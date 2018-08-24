We also need to create the OpenShift project/namespace where the application will run.

Here we'll use a separate inventory with a different `openshift_cluster_content` variable, notice that this template is coming from a url!

```
cat <<EOM >inventory/host_vars/bootstrap.yml
---
ansible_connection: local

openshift_cluster_content:
- object: projects
    content:
    - name: dev
      template: "https://raw.githubusercontent.com/redhat-cop/cluster-lifecycle/master/files/projectrequest/template.yml"
      template_action: create
      params: "{{ playbook_dir }}/params/projectrequests/project"
      tags:
      - projectrequests
      - projectrequests-dev
EOM
```{{execute}}

And now we'll create the parameters for this template...

```
cat <<EOM >params/projectrequests/project
NAMESPACE=ruby-example
NAMESPACE_DISPLAY_NAME="Ruby Example"
EOM
```{{execute}}

Again, feel free to run the `oc process` command to verify this template and params file are working correctly