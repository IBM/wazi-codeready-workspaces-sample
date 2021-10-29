## IBM Wazi Developer for Workspaces customization examples

The samples in this repository are used with the tutorial "Customizing IBM Wazi Developer for Workspaces devfile, plug-in registries, and sidecars" in the IBM Wazi Developer [user documentation](https://www.ibm.com/docs/en/wdfrhcw/1.4.0).

IBM® Wazi Developer for Workspaces is built on Red Hat® CodeReady Workspaces. It enables you to customize and add new plug-ins and devfiles to create a custom workspace. You can extend IBM Wazi Developer for Workspaces by customizing any of the following registries:

- Plug-in registry: You can add new plug-ins by customizing the IBM Wazi Developer for Workspaces plug-in registry. The default IDE in IBM Wazi Developer for Workspaces is Che-Theia. Che-Theia plug-ins add capabilities to the Che-Theia IDE and rely on plug-in APIs that are compatible with Visual Studio Code. As the plug-ins are isolated from the IDE, they can be packaged as files or containers to keep their own dependencies.
- Devfile registry: You can add new stacks by customizing the IBM Wazi Developer for Workspaces devfile registry. Stacks or workspace definitions are pre-configured CodeReady Workspaces with a dedicated set of tools that cover different developer personas. For example, you can pre-configure a workbench for testers with only the tools needed for their purposes.

You can obtain the necessary sources from the repository <https://github.com/IBM/wazi-codeready-workspaces> to create and deploy your customized version of IBM Wazi Developer for Workspaces. Refer to its readme file to learn more about what is in that repository.
