-> Minikube CLI: those will be used to start/stop/delete cluster.
-> Kubectl CLI: Configure the minikube cluster. (do whatever thing in the cluster)


* Minikube commands:
-> Start a cluster using the docker driver:
> minikube start --driver=docker 
![image](https://user-images.githubusercontent.com/4542664/127006369-9b522a0b-2d14-46fd-8aa2-ef304aea2383.png)


-> Get the status of the nodes:
In the following image, minikube is READY.
> kubectl get nodes
![image](https://user-images.githubusercontent.com/4542664/127025100-21e1a207-ae14-425c-89d8-06e6123ea2c1.png)


> minikube status
![image](https://user-images.githubusercontent.com/4542664/127176469-df8d80a2-77d4-4f5a-b79a-f404f36e9ae4.png)

> kubectl version  (we should see Client and server version, that means minikube is correctly configured.)
![image](https://user-images.githubusercontent.com/4542664/127176675-8e5110a2-5836-4d0a-823d-48606a4e0fc6.png)

> kubectl get pod  
(In this case I do not have pods)
![image](https://user-images.githubusercontent.com/4542664/127177633-24f2b39f-788e-4e35-8f97-cded9ef29569.png)

> kubectl get services
(this will show me all the current services)
![image](https://user-images.githubusercontent.com/4542664/127178245-5572d13d-cbd7-4a1b-a592-81e7f039fc05.png)

##Deplopyment:
Deployment will have all the "blueprint" to create pods:

-> Create a POD
You won't be able to create PODs, because PODs is an abstraction, you will create "Deployment", this is the command:
> kubectl create deployment NAME --image=image 
(The POD needs an image that's why we add the image)
Example: let's create an nginx deployment:
> kubectl create deployment nginx-depl --image=nginx
(The previous command called the deployment as nginx-depl, and it will download from docek-hub the image nginx)
![image](https://user-images.githubusercontent.com/4542664/127180617-8bc5d4d3-fb07-45df-8dd2-0086e483d00d.png)

-> get deployments:
> kubectl get deployment
![image](https://user-images.githubusercontent.com/4542664/127180785-8acaf648-d4f6-4187-a3a9-67572147397e.png)
it says:
READY 0/1 -> it means it is not ready yet.
Naw it is ready:
![image](https://user-images.githubusercontent.com/4542664/127181016-ece63d37-2605-4d3c-a23e-d2fa39fdbcb4.png)

-> Get PODs, top get the last deployment created.
Now, you will be able to see the pod (the deployment created)
![image](https://user-images.githubusercontent.com/4542664/127181193-29ddd9db-c579-4eb3-a880-114060316025.png)

##Replicas:
> kubectl get replicaset
> (Replicaset is managing the replicas of a pod, you do not have to create/update/delete replicaset, you will be working with deployments directly)
> ![image](https://user-images.githubusercontent.com/4542664/127181852-3f2b1229-c0bc-4540-9ba4-7d15c79724d0.png)

Summary:
"Deployment" manages a "Replicaset" which manages a "pod" which is an abstraction of a "container".
Everything below "deployment" is handled by kubernetes.

##Editing the image:
So, to edit the image, I will edit that in the deployment, not in the pod:
> kubectl edit deployment nginx-depl
(it will open a notepad with the configuration to edit properties of the deployment)
![image](https://user-images.githubusercontent.com/4542664/127183138-6dbb9fa2-9f27-44fc-a681-714ab26366ff.png)

I edited the nginx version to 1.16:
![image](https://user-images.githubusercontent.com/4542664/127183472-c29f9015-f517-42d9-ad40-da10c5903059.png)

Get the pods:
> kubectl get pod
(we will see that a new image is being created, that's the one with the new version)
![image](https://user-images.githubusercontent.com/4542664/127183733-afacdc75-721c-4552-9b0e-a262acb83333.png)

> kubectl get pod
(Now, we see the other pod is being terminated and our new pod is running)
![image](https://user-images.githubusercontent.com/4542664/127184024-915686a8-764f-41e4-b132-dfe879db4ce2.png)

> kubectl get pod
Finally the old pod is gone, we only see the new one.
![image](https://user-images.githubusercontent.com/4542664/127184134-1c81d8bd-8127-4dd9-b8f9-c2b9f8fd19d5.png)

> kubectl get replicaset
(the old one doews not have any pods in it and a new one has been created)
![image](https://user-images.githubusercontent.com/4542664/127184641-78e6f2d6-b668-4692-8fbc-4ea5961c6c58.png)

##Debugging pods:
< kubectl logs [Complete name of the pod]
> kubectl logs nginx-depl-7fc44fc5d4-fqrqq
For now, it is empty:
![image](https://user-images.githubusercontent.com/4542664/127186313-6d8de799-7087-4d4d-8388-1b4a1c6b2a5b.png)

Create a new image for mongo:
> kubctl create deployment mongo-depl --image=mongo
![image](https://user-images.githubusercontent.com/4542664/127186568-8a498c9f-147f-4456-90f7-81a28c727364.png)

> kubectl get pod
The pod is being created, when I try ot get logs it will crash because the pod is not running)
![image](https://user-images.githubusercontent.com/4542664/127187019-c24d8968-e306-4c1c-a4f0-5c137058d73c.png)

> kubectl describe pod [Name of the pod]
Using describe will get the complete status of the pod
![image](https://user-images.githubusercontent.com/4542664/127187447-eeff06e3-cc4c-461a-a031-a48ca5b02afb.png)
at the end you will see what is the current status, we are waiting for start.
![image](https://user-images.githubusercontent.com/4542664/127187559-18a8111b-ba3f-4b63-b3ab-2fd4e76695f5.png)

When the pod is running, the log command will work:
> kubectl logs [Pod name]
![image](https://user-images.githubusercontent.com/4542664/127187827-17af24e1-8a8d-47c3-a0e6-f620adb5a20b.png)

##Access the terminal of the pod:
> kubectl exec -it mongo-depl-xx -- bin/bash
![image](https://user-images.githubusercontent.com/4542664/127188571-bee6f647-084b-4996-baf6-6ad1d4cfa79e.png)

##Delete pod
> kubectl get deployment
![image](https://user-images.githubusercontent.com/4542664/127188885-8c02d294-d8bd-4a5a-8ac8-98ed8cfa903b.png)

> kubectl delete deployment mongo-depl
![image](https://user-images.githubusercontent.com/4542664/127189318-2665eb05-321c-4936-8690-fe5d174b60aa.png)
* deployment, replicaset and pod does not have any reference to the mongo.

##Create deployment using YAML file
> vi nginx-deployment.yaml
As soon as you create the YAML file:
![image](https://user-images.githubusercontent.com/4542664/127190352-98b02d83-0463-48dd-9099-2a9e84acc662.png)
> kubectl apply -f nginx-deployment.yaml

> vi nginx-deployment.yaml (edit the number of replicas) to 2
![image](https://user-images.githubusercontent.com/4542664/127191185-fd270748-018d-4d51-8fe9-dcf4ca64519a.png)


