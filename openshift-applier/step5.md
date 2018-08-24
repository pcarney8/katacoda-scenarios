To finish up the inventory, we need to update the hosts file to include the host_vars we just created.

```
cat <<EOM >inventory/hosts
[bootstrap]
bootstrap

[application]
application
EOM
```{{execute}}

In the next step we'll create the playbook and then run it.