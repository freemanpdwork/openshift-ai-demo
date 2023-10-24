# openshift-ai-demo

### Requirements
- 4 physical CPU cores
- 9 GB of free memory
- 35 GB of storage space
- Note: tested on MacBook Pro M1, 2020

### Install OpenShift Local
1. Follow instructions to install the latest release of OpenShift Local

https://access.redhat.com/documentation/en-us/red_hat_openshift_local/2.28/html/getting_started_guide/installing#installing_red_hat_openshift_local

- Note: don't forget to download pull secret. You'll need this to complete the following steps.

### Setup OpenShift Local
1. Run these commands
```shell
crc setup
crc start

note: copy and paste pull secret when prompted
```

### Login to OpenShift Local
1. Run these commands
```shell
eval $(crc oc-env)
oc login -u kubeadmin https://api.crc.testing:6443
oc whoami
```