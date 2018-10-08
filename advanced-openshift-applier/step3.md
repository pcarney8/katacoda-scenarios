This part should look familiar, BUT THERE'S A DIFFERENCE!

Like last time, these parameters match up with each Template to create a list of OpenShift objects...

But this time we will use them as our defaults!

Our `ruby-example-template` only has one parameter: `NAMESPACE_BUILD`. 

Let's create a parameter file to set this value:

```
echo 'NAMESPACE_BUILD=ruby-example' > params/ruby/build
```{{execute}}


Now we'll create the parameters for the Project template:

```
cat <<EOM >params/projectrequests/project
NAMESPACE=ruby-example
NAMESPACE_DISPLAY_NAME="Ruby Example"
EOM
```{{execute}}