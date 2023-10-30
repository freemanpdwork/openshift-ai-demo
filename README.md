# openshift-ai-demo
WIP

This is an example pet name generator app used in the OpenAI API [quickstart tutorial](https://platform.openai.com/docs/quickstart). It uses the [Next.js](https://nextjs.org/) framework with [React](https://reactjs.org/). These steps cover how to deploy the app on [OpenShift Local](https://developers.redhat.com/products/openshift-local/overview), however, it's also K8's agnostic. 

This project is based on https://github.com/openai/openai-quickstart-node

### Requirements
- 4 physical CPU cores
- 9 GB of free memory
- 35 GB of storage space
- quay.io account
- openai.com account, credits, and api key 
- Note: tested on MacBook Pro M1, 2020

### Install OpenShift Local
1. Follow the instructions to install the latest release of [OpenShift Local](https://access.redhat.com/documentation/en-us/red_hat_openshift_local/2.28/html/getting_started_guide/installing#installing_red_hat_openshift_local)
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
### Build container image example
```shell 
podman build -f Containerfile -t quay.io/<repository>/<repository_name>
quay.io/<repository>/<repository_name>
```

### Deploy container to 
```shell
oc create -f deployment.yaml
oc create -f service.yaml
oc create -f route.yaml
todo: add openai key secret and variable  
```

### Clean up
```shell
oc delete -f deployment.yaml
oc delete -f service.yaml
oc delete -f route.yaml
```

### Issues
```shell
Error: unable to start host networking: "could not find \"gvproxy\" in one of [/usr/local/opt/podman/libexec /opt/homebrew/bin /opt/homebrew/opt/podman/libexec /usr/local/bin /usr/local/libexec/podman /usr/local/lib/podman /usr/libexec/podman /usr/lib/podman $BINDIR/../libexec/podman].  To resolve this error, set the helper_binaries_dir key in the `[engine]` section of containers.conf to the directory containing your helper binaries."
```
#### Fix
```
1. Download gvproxy from the gvisor-tap-vsock release page. https://github.com/containers/gvisor-tap-vsock/releases
2. mv ~/Downloads/gvisor-darwin /opt/homebrew/bin/gvproxy
3. chmod 755 /opt/homebrew/bin/gvproxy
4. Add the helpers_binaries_dir entry to ~/.config/containers/conf
ex. 
[engine]
  helper_binaries_dir=["/opt/homebrew/bin/"]
```
