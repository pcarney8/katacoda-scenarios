To get started, let us login to the OpenShift cluster by running the following:

``oc login -u developer -p developer``

To begin, let's create a new directory and go into it.

``mkdir sample-applier; cd sample-applier``{{execute}}

To complete the generic project structure, we want to create the rest of these:

```
.
├── inventory
│   ├── group_vars
│   │   └── all.yml
│   ├── hosts
│   └── host_vars
│       ├── application.yml
│       └── bootstrap.yml
├── params
├── projectrequests
├── requirements.yml
└── templates
```

```
mkdir -p inventory/{group_vars,host_vars} params templates
touch inventory/group_vars/all.yml inventory/host_vars/{application.yml,bootstrap.yml} inventory/hosts
```{{execute}}