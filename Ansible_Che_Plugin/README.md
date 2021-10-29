## Wazi Developer for Workspaces Plugin example

This folder contains a sample for creating a custom plugin for IBM Wazi Developer for Workspaces. It defines a new sidecar that contains Red Hat Ansible executables as well as IBM's [Red Hat Ansible Certified Content for IBM Z](https://ibm.github.io/z_ansible_collections_doc/index.html). The plugin then also adds the Ansible VS Code extension together with the VS Code Python VS Code extension for supporting editing of Ansible playbooks directly in Wazi Developer for Workspaces.

### Building the sidecar image

To build the sidecar image

```bash
CONTAINER_REGISTRY=quay.io
USER_NAMESPACE=user
SIDECAR_IMAGE=ansible-zos
cd Ansible_Che_Plugin/sidecar
docker build -t ${CONTAINER_REGISTRY}/${USER_NAMESPACE}/${SIDECAR_IMAGE}:latest .
```

As you need to publish the image in an image registry replace the variables above with values required for a tag by your registry. If you do not have a registry and still want to try the plugin you can can use the image pre-published at `quay.io/wazi/ansible-zos:latest` for this example.

Typical commands to publish to a registry such as quay

```shell
docker login ${CONTAINER_REGISTRY}
docker push ${CONTAINER_REGISTRY}/${USER_NAMESPACE}/${SIDECAR_IMAGE}:latest
```

### To run the plugin

* If you published your own image, update the `devfile.yaml` and `plugin/meta.yaml` with the new tag used.
* Copy the `devfile.yaml` and `plugin/meta.yaml` to a public web server or public github repository
* In CodeReady Workspaces click on "Get Started" in the menu on the left.
* Select the "Custom Workspace" tab.
* In the form you see then just paste the URL to your devfile.yaml the field labelled "URL or devfile"  and click the "Load devfile" button.
* Review the contents of the yaml file and make changes if needed.
* Scroll down and click the "Create & Open" button.
