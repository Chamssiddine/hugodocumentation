---
title: "IAM GKE"
date: 2023-01-14T13:56:27+01:00
draft: false
---

1. create iam role

Create a new IAM role with the appropriate permissions for your developer. For example, you can use the roles/container.developer predefined role, which grants permissions to deploy and manage Kubernetes resources, but does not allow access to cluster administration. You can create a new role using the following command:

```bash
gcloud iam users create chams --display-name "Chamseddine Abderrahim" --email chamseddine.abderrahim@gmail.com
```
2. Assign the IAM role to your developer. You can do this by running the following command:
```bash 
gcloud projects add-iam-policy-binding remotedevenv-383413 --member=user:chamseddine.abderrahim@gmail.com --role=roles/container.developer

```
3. 

```bash
kubectl create namespace chams-namespace
```

4. create role-binding.yaml

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: chams-role-binding
  namespace: chams-namespace
subjects:
- kind: User
  name: chamseddine.abderrahim@gmail.com
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: view
  apiGroup: rbac.authorization.k8s.io
```

5. apply the configuration

```bash
kubectl apply -f role-binding.yaml
```