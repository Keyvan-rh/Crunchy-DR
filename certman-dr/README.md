# Crunchy-DR
### To setup the DR Crunchy cluster you need to setu the correct Certification
on the secound cluster to do this you need to:
* change directory to the certman-dr in the cloned directory.
* Login to first OCP cluster.
* Export the root-secret using the following command:
  
```shell
oc extract secret/root-secret --to=./tmp --confirm -n cert-manager
```
* Login to the 2nd OCP Cluster
* Create a root-secret using the following command:
  
```shell
oc create secret generic root-secret --from-file=tls.crt=./tmp/tls.crt --from-file=tls.key=./tmp/tls.key --from-file=ca.crt=./tmp/ca.crt -n cert-manager
```
* Create the ca-issuer:
  
```shell
oc create -k .
```

