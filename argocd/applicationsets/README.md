
ApplicationSets are a feature in ArgoCD that allows you to automatically create and manage multiple Applications based on a single declarative configuration. This can be particularly useful when you need to manage a large number of Applications or when you want to create Applications dynamically based on certain criteria or parameters.



You should consider using ApplicationSets in Argo CD when you have the following scenarios:

Managing multiple applications across environments If you have the same application deployed in different environments (e.g., dev, staging, prod), you can use an ApplicationSet to create and manage separate Applications for each environment. This way, you can easily sync and manage the application manifests across different environments from a single source.

Managing applications for different teams or projects If you have different teams or projects that require separate applications with different configurations, you can use an ApplicationSet to create and manage Applications for each team or project. This allows you to maintain separation of concerns and enable self-service for teams while still having centralized management through Argo CD.

Scaling applications across multiple clusters or regions If you need to deploy the same application across multiple Kubernetes clusters or different regions, you can use an ApplicationSet to create and manage Applications for each cluster or region. This helps you maintain consistency and simplify the deployment process across different infrastructure configurations.

Automating application creation based on dynamic parameters ApplicationSets allow you to use generators that can create Applications based on dynamic parameters, such as labels, annotations, or custom configurations. This can be useful when you need to automate the creation of Applications based on certain conditions or criteria.

Reducing duplication and improving maintainability Instead of manually creating and managing multiple Applications with similar configurations, you can use an ApplicationSet to define a template and generate Applications from it. This reduces duplication and improves maintainability by allowing you to make changes to the template, which will propagate to all generated Applications.

Enabling self-service application deployment ApplicationSets can be used to provide a self-service mechanism for teams or developers to deploy their applications without needing direct access to Argo CD. They can provide the necessary parameters or configurations, and the ApplicationSet will create and manage the Applications automatically.

In general, ApplicationSets are beneficial when you need to manage multiple Applications with similar or related configurations in a scalable and automated manner. They help simplify the management of complex application deployments and promote consistency across different environments, clusters, or teams.

However, if you only have a small number of applications with unique configurations, using individual Applications might be more straightforward. ApplicationSets are more valuable when you have a larger number of applications or when you need to automate and standardize the application creation process based on specific criteria or parameters.