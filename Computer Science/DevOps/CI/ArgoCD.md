<span style="color:#d65d0e">ArgoCD</span> <span style="color: #3588E9">--></span> declarative Continuous Delivery tool that makes CD easy to automate, audit, and understand. It follows the GitOps pattern of using Git repositories as the single source of truth for defining the desired application state. 

It reports deviations and providers visualizations to help developers manually and automatically sync the live state with the desire state.

ArgoCD, as a Kubernetes controller, monitors the current application state compared to the desired state, visualizes the differences, and ensures parity by automatically syncing. It automates the sunchronization of the desired state with each of teh specified target environments, 

- Argo CD was originally developed by Intuit, as they were looking for a lighter tool than Spinnaker that would improve build and deployment times and streamline their GitOps workflow. The UI is well made and easy to use and integrates well with a variety of CI tools such as Jenkins, GitHub Actions, CircleCI, and more.

concepts:
- 

- <strong style="color: white">Features:</strong>
	- Declarative application deployment
	- Continuous Monitoring Synchronization
	- Single Sign-On (SSO) Integrations
	- Rollback and Controlled Roll-outs
	- Reusable Application Configurations Patterns
	- Robust Role-based Access Control (RBAC)