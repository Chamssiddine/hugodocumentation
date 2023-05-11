---
title: "RBAC with k8s"
date: 2023-01-14T14:56:27+01:00
draft: false
---

1. Create a namespace for the developer

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: developer

```


2. Create Role:

```yaml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: developer-role
  namespace: developer
rules:
- apiGroups: [""]
  resources: ["pods", "services"]
  verbs: ["get", "list", "watch"]

```
3. Bind the role to the developer user:

```yaml
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: developer-rolebinding
  namespace: developer
subjects:
- kind: User
  name: developer-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: developer-role
  apiGroup: rbac.authorization.k8s.io

```

4. Apply the configuration

```ruby
kubectl apply -f namespace.yaml
kubectl apply -f role.yaml
kubectl apply -f rolebinding.yaml
```

4. Generate the certifact for the developer
```bash
openssl genrsa -out developer.key 2048
openssl req -new -key developer.key -out developer.csr -subj "/CN=developer-user/O=developer-group"

```
now sign the certificate

```bash 
openssl x509 -req -in developer.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out developer.crt -days 365
```
4. Create the kubeconfig File:
```bash
# Set the cluster configuration and write to a new kubeconfig file
kubectl config set-cluster primary --server=https://<cluster-api-server-url> --certificate-authority=ca.crt --embed-certs=true --kubeconfig=~/Documents/sensitive/developer-kubeconfig.yaml

# Set the user configuration and append to the new kubeconfig file
kubectl config set-credentials developer-user --client-key=developer.key --client-certificate=developer.crt --embed-certs=true --kubeconfig=~/Documents/sensitive/developer-kubeconfig.yaml

# Set the context configuration and append to the new kubeconfig file
kubectl config set-context developer-context --cluster=primary --user=developer-user --kubeconfig=~/Documents/sensitive/developer-kubeconfig.yaml

# Use the newly created context and kubeconfig file
kubectl config use-context developer-context --kubeconfig=~/Documents/sensitive/developer-kubeconfig.yaml
```