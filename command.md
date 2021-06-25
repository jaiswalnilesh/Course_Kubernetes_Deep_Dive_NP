Deploying hpademo.yml
>kubectl apply -f hpademo.yml

# It will take time to provisioned, wait for sometime

Check the state of deployment
>kubectl get deploy --namespace acg-ns

Check the state of hpa
>kubectl get hpa --namespace acg-ns

As per requirement, it will create one node
check it with below command
>kubectl get nodes

# Now let's stress it
Open new terminal and run below command, it hammer the webserver pod

> kubectl run -i --tty loader --image=busybox /bin/sh
> while true; do get -q -O- HTTP://acg-lb.acg-ns.svc.cluster.local; done



Now check the status on another screen for stress to take action

>kubectl get hpa --namespace acg-ns

>kubectl get hpa --namespace acg-ns --watch

We may see replica count going up

check the deployment
>kubctl get deploy --namespace acg-ns

You can also dump the deployment yml using below command
>kubectl get deploy --namespace acg-ns -o yaml

Check when more demand may push pods to pending

-----Cluster Autoscaler

Make sure you create cluster environment using gke or other vendor or local cluster, here I am using gke
from your local machine connect to gke cluster
gcloud container clusters get-credentials acg-autoscale --zone europe-west2-b --project acg1-206211

The above command will configure kubectl 


kubectl apply -f autoscale.yml


