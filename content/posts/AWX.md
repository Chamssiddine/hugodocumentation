---
title: "AWX"
date: 2023-01-17T14:56:04+01:00
draft: false
---
# AWX
## How to install AWX using kubernetes operator
To install AWX using Kubernetes Operator, follow these steps:

1. Navigate to the awx-operator directory:

```bash
$ cd helm_charts/awx_chart/awx-operator
```

2. Verify the content of the following files:

- In kustomization.yaml, you can specify the version of AWX operator. 
```
 kustomization.yaml 
```
- In awx.yml, you can modify the specs of AWX to your needs.
```
 awx.yml 
```

3. Run the kustomize command to build the Kubernetes manifest and apply it:
```
$ kustomize build . | kubectl apply -f -
```
4. To get the initial passowrd type in 

```
$ kubectl get secret awx-admin-password -n awx -o jsonpath="{.data.password}" | base64 --decode ; echo
```

**IMPORTANT**: It may take some time to create the pods for AWX. It will create the AWX controller manager first. If it takes longer than expected, retype the same command until you see the 4 replicas of AWX. To check if the pods are created or not, type in the following command:
```ruby
kubectl get pods -n awx -w
```

# How to Integrate Keycloak with AWX
## AWX SIDE
1. Navigate to setttings -> Miscellaneous System settings

2. Edit Base URL of the service to your base URL or IP

3. Go back to Settings, then SAML settings and replace the fields as shown below:
* SAML Service Provider Entity ID

```
https://keycloakdomainname

```

* SAML Service Provider Public Certificate
* SAML Service Provider Private Key

- Generate a certificate and Public key by typing in :
```
$ openssl req -new -x509 -days 3650 -nodes -out saml.crt -keyout saml.key

```

* SAML Service Provider Organization Info:
```
{
  "en-US": {
    "url": "http://keycloakserviceip",
    "name": "keycloak",
    "displayname": "keycloak"
  }
}
```

* Specify SAML Service Provider Technical Contact:
```
{
  "emailAddress": "chamseddine.abderrahim@gmail.com",
  "givenName": "chamseddine"
}
```
* Specify Service Provider Support Contact:
```
{
  "emailAddress": "chamseddine.abderrahim@gmail.com",
  "givenName": "chamseddine"
}
```

* Specify SAML Enabled Identity Provider:
```
{
  "keycloak": {
    "x509cert": "certificatewithoutbreakinglines",
    "attr_first_name": "first_name",
    "attr_email": "email",
    "url": "http://keycloakserviceip/auth/realms/tower/protocol/saml",
    "attr_user_permanent_id": "name_id",
    "entity_id": "http://keycloakserviceip/auth/realms/tower",
    "attr_groups": "groups",
    "attr_last_name": "last_name",
    "attr_username": "username"
  }
}
```

* Specify SAML Organization Map:
```
{
  "Default": {
    "users": true
  },
  "Systems Engineering": {
    "remove_users": false,
    "remove_admins": false,
    "users": true,
    "admins": [
      "chamseddine.abderrahim@gmail.com"
    ]
  }
}
```
![awx](/awxsettingstochange.m4v)
* verify 

```
$ curl -k -L http://AwxServiceIP/sso/metadata/saml/ > awx-keycloak.xml

```

## Keycloak Side

* Create Your REALM named: tower

* Import the "awx-keycloak.xml" to your REALM

![createrealm](/createrealminkeycloak.mov)

* Add Your certificate and Private key to your REALME 

![thumbnail](/keycloakawxone.m4v)

* Add Mappers for the saml request nagivate to infrastructure/modules/awxsaml and type in:

```
terraform init
terraform apply
```
NOTE: Change the variable values inside variables.tf file to match your service url etc....

* Verify the SSO is working
![test](/verifyeverythingandtestsso.m4v)
![finishedtouches](/verifyeverythingandtestsso.m4v)
# Use AWX to prepare your environment 
* Adding Dynamic Inventory 

* Adding Ansible Playbook