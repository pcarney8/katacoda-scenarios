## Username and Password are great, but let's encrypt a ssh private key!

Let's update the `group_vars/all.yml` to look like:

```
- object: secrets
  content:
  - name: user-pass
    template: "{{ inventory_dir }}/../templates/secrets/secret-user-pass-template.yml"
    params_from_vars:
      SECRET_NAME: user-pass
      USERNAME: "{{ encrypted_username | b64encode }}"
      PASSWORD: "{{ encrypted_password | b64encode }}"
    action: create
    ignore_unknown_parameters: false
    namespace: concentrated-dark-matter-secret
    tags:
      - secrets
      - secrets-user-pass
```{{copy}}

Notice the ` | b64encode }}` 

The ansible filter will encode it for us! No need to change your encrypted username and password! 

And we'll run it once more:
``ansible-playbook -i inventory/ apply.yml``{{execute}} 

You should see something like this:
```
PLAY RECAP ****************************************************************
localhost                  : ok=20   changed=2    unreachable=0    failed=0
```{{}}

If you want, go over to the `Dashboard` tab in this environment

Login with the credentials: 

```
user: developer
pass: developer
```

You should see the `concentrated-dark-matter-secret` project! 

If you navigate to the left panel and go to Resources -> Secrets you should see our secret!

Let's keep going...

