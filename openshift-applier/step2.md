###For this tutorial, we are going to use an existing Ruby OpenShift Template. 

In many cases you may want your own custom template, but the process is the same.

####First you'll need to find the name of the template you want to pull in:

``oc get templates -n openshift``{{execute}}

You should see the following output:
```
NAME                    DESCRIPTION   PARAMETERS    OBJECTS
ruby-example-template                 1 (1 blank)   6
```

####`ruby-example-template` is the name of the template we're going to pull down as a template file into the `templates` directory.

```
oc export template ruby-example-template -n openshift -o yaml > templates/app/ruby.yml
```{{execute}}

####To checkout what the template looks like, run the following:

``cat templates/app/ruby.yml``{{execute}}

There are parameters that match up with the Template to then create a list of OpenShift objects

Our `ruby-example-template` only has one parameter: `BUILD_NAMESPACE`. 

####Let's create a parameter file to set this value:

```
echo 'BUILD_NAMESPACE=ruby-example' > params/ruby/build
```{{execute}}

In the next step we'll start populating the inventory.