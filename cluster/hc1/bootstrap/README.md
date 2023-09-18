# Bootstrap


- Install External Secrets Operator


## Deploy OnePassword Connect


```
oc create secret generic connect-server-credentials \
  -n onepassword-connect \
  --from-file=1password-credentials.json=$HOME/Downloads/1password-credentials.json

```





export OP_API_TOKEN="eyJhbGciOiJFUzI1NiIsImtpZCI6InNwcTdncGg3cjJzM29jZTdzNDNnZTZ4dnBpIiwidHlwIjoiSldUIn0.eyIxcGFzc3dvcmQuY29tL2F1dWlkIjoiS0VKVTNJUFpPWkJEQk9CT1NYRVBTQUg2NjQiLCIxcGFzc3dvcmQuY29tL3Rva2VuIjoiVk4zQXJSZTZzN0ZHMmVLSzdIcEhkZERCTkEtMl9MSC0iLCIxcGFzc3dvcmQuY29tL2Z0cyI6WyJ2YXVsdGFjY2VzcyJdLCIxcGFzc3dvcmQuY29tL3Z0cyI6W3sidSI6Imh4Z2ZuYTRveXprc3lycWR5cXozYnpuZHhlIiwiYSI6NDh9XSwiYXVkIjpbImNvbS4xcGFzc3dvcmQuY29ubmVjdCJdLCJzdWIiOiI1STQ3RDVQUllWQ0lYR1dON0YyM0lJNlJLQSIsImlhdCI6MTY4MDM2NTQ0OCwiaXNzIjoiY29tLjFwYXNzd29yZC5iNSIsImp0aSI6ImdnYmk1c3d1anJscHpqanZtbTJmZjd6bnV1In0.25PkWH3LrtUN5vH1HnjfDPsbI-7b8tXG3DmY-Uh4e6MwDHSQPjthZx64KOKaNpaN2oHeEBm2DOPDnqfJBQ1p2Q"

```
curl \
  -X GET \
  -H "Accept: application/json" \
  -H "Authorization: Bearer $OP_API_TOKEN" \
  https://api-onepassword-connect.apps.onlogic.bohne.io/v1/vaults
```


oc create secret generic onepassword-api-token \
 -n external-secrets-operator \
 --from-literal=token=$OP_API_TOKEN




