Because the `params_from_vars` variable overwrote the `params` file variable, and the `NAMESPACE_BUILD: not-a-ruby-example` is not the correct namespace!

The easy way to fix this would be to change this:

`NAMESPACE_BUILD: not-a-ruby-example` 

to this:

`NAMESPACE_BUILD: ruby-example`

But let's fix our inventory using dynamic variables in a different way...