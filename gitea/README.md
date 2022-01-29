# Gitea Operator and Instance

This is composed of a `Policy` (create the Gitea operator `CatalogSource` and `Subsription`), and an `Application` (create the Gitea `Namespace` and `Gitea` instance).

This uses the [Gitea Operator](https://github.com/redhat-gpte-devopsautomation/gitea-operator) - great for demos!

To add the policy and application to your ACM instance in one shot:

```
oc apply -k https://github.com/redhat-canada/acm-catalog/gitea
```

To deploy the operator and demo instance, add the following label to a cluster:

```
demo=gitops
```

The default Gitea instance can be found in the `manifests` directory.
