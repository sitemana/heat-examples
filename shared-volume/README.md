# Shared volume example

We will build two stacks:

* a persistent volume
* a stack using the created volume as a shared storage via NFS

This way we can keep our data during several livetimes of an application stack. If you delete the first stack, the persistent volume will be destroyed. Be careful!

## Start volume stack first

```shell
openstack stack create -t persistent_volume.yaml volume_storage
```

## Get cinder volume ID

```shell
openstack volume list
```

## Paste Cinder volume ID into the parameter section in the stack-env.yaml file

```shell
parameters:

...

volume_id: "6f603cae-10e2-4b32-b1ad-a285e5edf2ae"
```


## Paste your SSH Key in the stack-env.yaml file

```shell
parameters:

...

ssh_keys:
    - 'ssh-rsa AAAAB3NzaC1yc2...
```

## Create NFS client/server stack

Create the stack with the following command

```shell
openstack stack create -t stack.yaml -e stack-env.yaml demo_stack
```

