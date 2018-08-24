Now we need the our Openshift-Applier role from GitHub, let's create the `requirements.yml` file

https://github.com/redhat-cop/openshift-applier

```
cat <<EOM >requirements.yml
- name: openshift-applier
    scm: git
    src: https://github.com/redhat-cop/openshift-applier
    version: v2.0.0
EOM
```{{execute}}

First pull down the ansible-galaxy requirements into the `roles` directory:

``ansible-galaxy install -r requirements.yml -p roles``{{execute}}

Then start the run:

``ansible-playbook -i inventory apply.yml -e "target=bootstrap,application"``{{execute}}

If that is successful you should she:

```
changed: 123432
etc TODO: ADD THESE HERE
```

