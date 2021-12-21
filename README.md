# Red Hat Advanced Cluster Management (ACM) Catalog

A catalog of Policies and Applications used by Red Hat Canada SAs for demos and experimentation.  This is *not* a supported repository.

## Installing Advanced Cluster Management for Kubernets

For an easy way to deploy ACM to your "hub" cluster, you can either manually deploy the operator through the OperatorHub integration in OpenShift, or you can deploy with the command line.

```
# Deploy the Operator.
oc apply -k https://github.com/redhat-cop/gitops-catalog/advanced-cluster-management/operator/overlays/release-2.4

# After the operator is installed, install an instance.
oc apply -k https://github.com/redhat-cop/gitops-catalog/advanced-cluster-management/instance/base
```

ACM will take some time to deploy.  Once complete, you can start applying different policy and application catalog entries to have them added to your ACM instance.
