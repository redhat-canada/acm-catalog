# Manual Steps for Truseted Certificates

If you want ACS to have a trusted certificate for it's route, you will need to first run the following manual steps:

1. Login to your cluster with `oc` as a cluster-admin.
2. Find the name of your router certificate secrets.
```
oc get secret -n openshift-ingress
```
3. Copy the secret to your machine.
```
oc get secret ingress-certs-2021-12-21 -n openshift-ingress -o yaml > ingress-cert.yaml
```
4. Edit the file and change the secret name to `ingress-certs` then remove:
    * `namespace` 
    * `creationTimestamp`
    * `resourceVersion`
    * `uid`
5. Create a new namespace to hold a copy of the cert, then create the certificat in that namespace.
```
oc new-project stackrox-secrets
oc apply -f ingress-cert.yaml -n stackrox-secrets
```

Now you can use the `acs-central-policy-with-certs` policy to deploy ACS with good certificates.