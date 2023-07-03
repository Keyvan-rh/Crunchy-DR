# Crunchy-DR
### Prerequisite

* Install redhat cert-manager operator
* Install Crunchy database operator
  
### To setup the DR Crunchy cluster you need to setup the correct issuer on the secound cluster to do this you need to:
* Change directory to the certman-dr in the cloned directory.
* Login to first openshift cluster.
* Export the created root-secret in cert-manager project which was created when you setup the primary crunchy cluser using the following command:
  
```shell
oc extract secret/root-secret --to=./tmp --confirm -n cert-manager
```
* Login to the 2nd openshift Cluster
* Create a root-secret using the following command in cert-manager project:
  
```shell
oc create secret generic root-secret --from-file=tls.crt=./tmp/tls.crt --from-file=tls.key=./tmp/tls.key --from-file=ca.crt=./tmp/ca.crt -n cert-manager
```
* Create the ca-issuer:
  
```shell
oc create -k .
```

