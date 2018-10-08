## Let's jump right into dynamic parameters!

If you remember from the first tutorial, if we combine a template with a parameters file, we use the `oc process` command. 

```
oc process --local -f templates/app/ruby.yml --param-file params/ruby/build
```{{execute}}

From there we put the template and the static parameter file together, and it looked like this:
```
openshift_cluster_content:
- object: projects
  content:
  - name: dev
    template: "{{ inventory_dir }}/../templates/project/projectrequest-template.yml"
    params: "{{ inventory_dir }}/../params/projectrequests/project"
    action: create
    ignore_unknown_parameters: false
    tags:
      - projectrequests
      - projectrequests-dev
```{{}}

Take note of:
```
     template: "{{ inventory_dir }}/../templates/project/projectrequest-template.yml"
     params: "{{ inventory_dir }}/../params/projectrequests/project"
```{{}}

And how it points to a file

Now, let's go ahead and make it dynamic! 

Run this command to create our group_vars file:

```
cat <<EOM >inventory/group_vars/all.yml
---
ansible_connection: local

openshift_cluster_content:
- object: projects
  content:
  - name: dev
    template: "{{ inventory_dir }}/../templates/project/projectrequest-template.yml"
    params_from_vars:
      NAMESPACE: ruby-example
      NAMESPACE_DISPLAY_NAME: "Ruby Example" 
    action: create
    tags:
      - projectrequests
      - projectrequests-dev
EOM
```{{execute}}

### You should notice that our static `params` file has become:

```
    template: "{{ inventory_dir }}/../templates/project/projectrequest-template.yml"
    params_from_vars:
      NAMESPACE: ruby-example
      NAMESPACE_DISPLAY_NAME: "Ruby Example" 
```{{}}

This is great! Why? Because now we can use [Ansible variables](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html) for more dynamic uses! 
