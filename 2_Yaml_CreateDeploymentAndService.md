All yaml contains 3 sections:
* metadata
* specification : The specification part depends on the specific kind (deployment, service)
* status : added automatically by kubernetes

The specification part depends on the specific kind (deployment, service)

* Deployment:
Example:
![image](https://user-images.githubusercontent.com/4542664/127194115-f1c08e82-9ad6-4fce-aaff-9361d1a44624.png)

Our application is inside the specification (this is like a configuration file inside another conf file)
![image](https://user-images.githubusercontent.com/4542664/127195355-5fcef20d-adcd-49f9-8e43-a2064d1a50c4.png)



* Service
Example:
![image](https://user-images.githubusercontent.com/4542664/127194319-350a4788-ac91-419d-979a-05de0bee5ae8.png)

---

Status:
it will be added automatiaclly depending on the current statusthat's data comes from etcd, example:
![image](https://user-images.githubusercontent.com/4542664/127194921-32cc0ea0-2dcf-4759-9c83-fc067d8f2a90.png)
