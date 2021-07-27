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

-> Create a POD
You won't be able to create PODs, because PODs is an abstraction, you will create "Deployment", this is the command:
> kubectl create deployment NAME --image=image 
(The POD needs an image

> 
