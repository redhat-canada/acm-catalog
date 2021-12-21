# Manual Steps for Truseted Certificates

If you want ACS to have a trusted certificate for it's route, you will need to first run the following manual steps:

1. Login to your cluster with `oc` as a cluster-admin.
2. Pre-create the `stackrox` namespace.
```
# Use "adm" to avoid any quotas/limits associated with new project template.
oc adm new-project stackrox
```
3. Find the name of your router certificate secrets.
```
oc get secret -n openshift-ingress
```
4. Create cert and key pem files locally.
```
oc get secret <ingress cert name> -n openshift-ingress \
  -o jsonpath="{.data.tls\.crt}" \
  | base64 -d \
  > cert.pem  

oc get secret <ingress cert name> -n openshift-ingress \
  -o jsonpath="{.data.tls\.key}" \
  | base64 -d \
  > key.pem
```
5. Create a default tls secret in the `stackrox` namespace.
```
oc -n stackrox create secret tls central-default-tls-cert \
  --cert cert.pem \
  --key key.pem \
  --dry-run -o yaml | oc apply -f -
```

Done!  Now, when you create a "Central" instance, it should automatically pick up your certificates.  No more self-signed certs for Central.