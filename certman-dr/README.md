# Crunchy-DR
To setup the DR Crunchy cluster you need to setu the correct Certification
on the secound cluster to do this you need to:
 0. cd to the certman-dr in the cloned directory.
 1. Login to first OCP cluster.
 2. Export the root-secret using the following command:
	oc extract secret/root-secret --to=./tmp --confirm -n cert-manager
 3. Login to the 2nd OCP Cluster
 4. Create a root-secret using the following command:
        oc create secret generic root-secret --from-file=tls.crt=./tmp/tls.crt --from-file=tls.key=./tmp/tls.key --from-file=ca.crt=./tmp/ca.crt -n cert-manager
 4. Create the ca-issuer:
        oc create -k .  
