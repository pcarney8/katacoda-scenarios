## Let's get our SECRETS templates! 

``oc get templates -n openshift``{{execute}}

You should see the following output:
```
NAME                      DESCRIPTION               PARAMETERS    OBJECTS
secret-user-pass-template                           3 (3 blank)   1
secret-ssh-private-key-template                     2 (2 blank)   1
```

First let's get the Secret Template for Username & Password!
```
oc export template secret-user-pass-template -n openshift -o yaml > templates/secrets/secret-user-pass-template.yml
```{{execute}}

And now get the Secret Template for SSH Private Keys!
```
oc export template secret-ssh-private-key-template -n openshift -o yaml > templates/secrets/secret-ssh-private-key-template.yml
```{{execute}}
