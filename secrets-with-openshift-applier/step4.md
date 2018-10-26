## Now, let's go ahead and create our encrypted strings!

In our `secret-user-pass-template.yml` we have a couple of parameters: `USERNAME` and `PASSWORD`, so let's encrypt both values! 
```
echo "rickSanchez01" | ansible-vault encrypt_string --stdin-name 'encrypted_username' >> encrypted-secrets.yml
```{{execute}}

There's a couple things to note here:

1. We are passing into ansible-vault command line using `echo`
2. `encrypt_string` will encrypt a string, not a file
3. `--stdin-name` creates the variable name

Now let's encrypt the password and add it to the same file
```
echo "m0rtyIsTheB3st" | ansible-vault encrypt_string --stdin-name 'encrypted_password' >> encrypted-secrets.yml
```{{execute}}

Have a look at what was created using:
```
cat encrypted-secrets.yml
```{{execute}}

