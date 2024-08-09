# Bootstrap


- Install External Secrets Operator
- Install OpemShift GitOps 

## Deploy OnePassword Connect


- https://developer.1password.com/docs/connect/get-started


```
oc adm policy add-scc-to-user nonroot-v2 -z default
helm repo add 1password https://1password.github.io/connect-helm-charts/
helm install connect 1password/connect --set-file connect.credentials=1password-credentials.json    
```



## Deploy external secret operator

* `oc new-project external-secrets-operator`
* Create OperatorConfig CR


```bash
oc create secret generic onepassword-api-token \
 -n external-secrets-operator \
 --from-literal=token=$OP_API_TOKEN
```

```yaml
apiVersion: external-secrets.io/v1beta1
kind: ClusterSecretStore
metadata:
  name: onepassword-container
spec:
  provider:
    onepassword:
      auth:
        secretRef:
          connectTokenSecretRef:
            key: token
            name: onepassword-api-token
            namespace: external-secrets-operator
      connectHost: http://onepassword-connect.onepassword-connect.svc.cluster.local:8080/
      vaults:
        container: 1
```

## Configure ArgoCD/GitOps

```bash
oc apply -f argocd/Application.yaml
```
