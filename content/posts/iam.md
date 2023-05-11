---
title: "Identity & Access Managment GKE"
date: 2023-01-14T13:56:27+01:00
draft: false
---
# Developer Access to GKE

We will add a our developer to access his dedicated well isolated namespace in the shared gke cluster 
1. Assign the IAM role to your developer

Create a new IAM role with the appropriate permissions for your developer. For example, you can use the roles/container.developer predefined role, which grants permissions to deploy and manage Kubernetes resources, but does not allow access to cluster administration. You can create a new role using the following command:

```bash
gcloud projects add-iam-policy-binding remotedevenv-383413 \
--member=user:chamseddine.abderrahim@gmail.com \
--role='roles/container.developer'
```
3. Create the namespace for your developer

```bash
kubectl create namespace developerone
```
4. Create Role for developerone using RBAC 
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer-role
  namespace: developerone
rules:
- apiGroups: [""]
  resources:
  - pods
  - services
  - deployments
  - configmaps
  - secrets
  - persistentvolumeclaims
  - ingresses
  - jobs
  - cronjobs
  - replicasets
  - statefulsets
  - daemonsets
  verbs:
  - get
  - list
  - watch
  - create
  - update
  - patch
  - delete
```

5. create role-binding.yaml
- file name: role-binding.yaml
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: developer-binding
  namespace: developerone
subjects:
- kind: User
  name: chamseddine.abderrahim@gmail.com    # Replace with the developer Email
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: developer-role
  apiGroup: rbac.authorization.k8s.io
```

5. apply the configuration

```bash
kubectl apply -f role.yaml role-binding.yaml
```

