argocd app create my-app --file app.yaml
argocd app sync my-app




In this case, the deployment-patch.yaml file will patch the base deployment.yaml by setting the number of replicas to 1 for the development environment.


For example, in the overlays/dev/ directory, we have a deployment-patch.yaml file that patches the base deployment by modifying the number of replicas:

```yaml
# overlays/dev/deployment-patch.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 1
```
The overlays/dev/kustomization.yaml file specifies how the overlay should be applied:
```yaml
# overlays/dev/kustomization.yaml
resources:
- ../../base
patchesStrategicMerge:
- deployment-patch.yaml
```
In this case, the deployment-patch.yaml file will patch the base deployment.yaml by setting the number of replicas to 1 for the development environment.

ArgoCD Application Manifest (app.yaml): The app.yaml file is the ArgoCD Application manifest that defines the application and its source and destination configurations.

```yaml
# app.yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: my-app
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/your-repo/my-app-repo.git
    targetRevision: main
    path: overlays/dev
  destination:
    server: https://kubernetes.default.svc
    namespace: my-app
```
In this example, the source.path is set to overlays/dev, which means ArgoCD will monitor the overlays/dev/ directory in the Git repository for changes and apply the manifests from that directory to the specified destination.

When you sync the ArgoCD Application, it will apply the base manifests from base/ and then apply the overlays/dev/ overlay on top of the base. This includes the deployment-patch.yaml patch, which modifies the number of replicas for the deployment in the development environment.

Using Kustomize and overlays in this manner allows you to maintain a consistent base set of manifests and selectively apply environment-specific customizations through patches or additional resources. This approach promotes code reusability and maintainability while enabling environment-specific configurations


