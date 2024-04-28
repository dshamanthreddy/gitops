
When you create an Application in ArgoCD, it automatically adds a finalizer to the resources managed by that Application. For example, consider the following Deployment resource:
Removing the finalizer: After performing the necessary cleanup tasks, ArgoCD removes the finalizer from the resources, allowing them to be safely deleted by Kubernetes.

In ArgoCD, a finalizer is a mechanism used to control the deletion process of Kubernetes resources managed by ArgoCD. It ensures that certain cleanup tasks or prerequisites are performed before the resource is completely deleted.

When you create an Application in ArgoCD, it automatically adds a finalizer to the corresponding Kubernetes resources (e.g., Deployments, Services, ConfigMaps) that are part of that Application. This finalizer is essentially a key that tells Kubernetes not to remove the resource until certain conditions are met.

The purpose of the finalizer in ArgoCD is to prevent accidental deletion of resources that are managed by ArgoCD. When you attempt to delete an Application in ArgoCD, the finalizer ensures that the resources associated with that Application are not immediately deleted. Instead, ArgoCD first performs a series of cleanup tasks, such as:

Pruning resources: ArgoCD checks if there are any resources that were previously deployed but are no longer present in the Git repository. If such resources exist, ArgoCD will prune (delete) them from the cluster.

Finalizing resources: ArgoCD finalizes the resources by removing any annotations, labels, or other metadata related to ArgoCD management.

Removing the finalizer: After performing the necessary cleanup tasks, ArgoCD removes the finalizer from the resources, allowing them to be safely deleted by Kubernetes.

This process ensures that resources are consistently managed and deleted in a controlled manner by ArgoCD, preventing potential issues like orphaned resources or resource leaks.

It's important to note that the finalizer mechanism is a built-in feature of ArgoCD and is automatically applied when you create an Application. You don't need to explicitly configure or manage the finalizers unless you have specific requirements or want to override the default behavior.

However, in some cases, you may need to manually remove the finalizer if the deletion process gets stuck or if you want to forcefully delete an Application and its resources. This can be done using the ArgoCD CLI or by directly modifying the Kubernetes resources.


