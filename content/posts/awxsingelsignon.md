---
title: "AWX SSO"
date: 2023-01-17T14:56:04+01:00
draft: false

---

## AWX Side
# AWX Single Sign On with keycloak

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
  "RHSSO": {
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

* Specify SAML Organization Map
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

* verify 

```
$ curl -k -L http://AwxServiceIP/sso/metadata/saml/ > client-import.xml

```

# Keycloak Side



![thumbnail](/thumbnail.png)