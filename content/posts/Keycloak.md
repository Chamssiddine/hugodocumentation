---
title: "Keycloak"
date: 2023-01-14T14:56:27+01:00
draft: false
---

1. Navigate to the Keycloak Helm Chart directory in your Git repo:

  `$ cd helm_charts/keycloak_chart` 

2. Add the Codecentric Helm repo:

```
 helm repo add codecentric 
```

3. Install Keycloak using the Helm Chart:

I have provided chart values that are customized for our needs, but you can make changes to suit your specific requirements. Use the following command to deploy Keycloak:

```
 helm install keycloak codecentric/keycloak -f keycloak_values.yaml
```

That's it! Your Keycloak instance should now be up and running, you can access it with the Keycloak Service IP.