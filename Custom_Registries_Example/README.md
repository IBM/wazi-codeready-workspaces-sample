## A rebuild of custom registries example for running a custom workspace

This is a little more work, however, the benefit is an easier end-user experience. This example assumes the sidecar from the first example was already built and pushed.

* Clone the [Wazi Codeready Workspaces](https://github.com/IBM/wazi-codeready-workspaces) repository

    ```shell
    git clone git@github.com:IBM/wazi-codeready-workspaces.git
    ```

* Copy new files and update index.json

   ```shell
   SOURCE_ROOT=../../../custom-che-registries/02_Custom_Registries_Example
   cd wazi-codeready-workspaces

   # Devfiles
   cd dependencies/che-devfile-registry
   cp -Rf ${SOURCE_ROOT}/devfiles/ ./devfiles/
   cp -Rf ${SOURCE_ROOT}/images/ ./images/
   cd ../..

   # Plugin
   cd dependencies/che-plugin-registry
   cp -Rf ${SOURCE_ROOT}/v3/ ./v3/
   cd ../..
   ```

* Build and Push the registry images

  ```shell
  CONTAINER_REGISTRY=quay.io
  USER_NAMESPACE=user
  DEVFILE_IMAGE=devfile-registry
  PLUGIN_IMAGE=plugin-registry
  DEVFILE_DOCKERFILE=./dependencies/che-devfile-registry/build/dockerfiles/Dockerfile
  PLUGIN_DOCKERFILE=./dependencies/che-plugin-registry/build/dockerfiles/Dockerfile

  docker login ${CONTAINER_REGISTRY}

  docker build -t ${CONTAINER_REGISTRY}/${USER_NAMESPACE}/${DEVFILE_IMAGE}:latest -f ${DEVFILE_DOCKERFILE} --target "registry" ./dependencies/che-devfile-registry/
  docker build -t ${CONTAINER_REGISTRY}/${USER_NAMESPACE}/${PLUGIN_IMAGE}:latest -f ${PLUGIN_DOCKERFILE} --target "registry" ./dependencies/che-plugin-registry/

  docker push ${CONTAINER_REGISTRY}/${USER_NAMESPACE}/${DEVFILE_IMAGE}:latest
  docker push ${CONTAINER_REGISTRY}/${USER_NAMESPACE}/${PLUGIN_IMAGE}:latest
  ```

Recreate the instance using the custom registries. Under the **Server** sections enter the respective custom registry images

* `Devfile Registry Image` -- __devfileRegistryImage__
* `Plugin Registry Image`  -- __pluginRegistryImage__
