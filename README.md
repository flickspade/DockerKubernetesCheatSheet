# DockerKubernetesCheatSheet
Docker and Kubernetes cheat sheet for Beginners
DOCKER CHEATSHEET

building docker image from a file :- docker build -t capitalmarkettec/commandsservice .
running a docker file :- docker run -p [port(container):port(applicationRunning PORT)] 5084: 6031 Username/appName
pushing the file in local hub:- docker push Username/appName


KUBERNETES CHEATSHEET

------------------DEPLOYMENT--------------------(EX) 			------------COMMANDS TO APPLY, DELETE AND RESTART CONTAINERS---------------------------		
apiVersion: apps/v1							------APPLY----	
kind: Deployment								kubectl apply -f platforms-np-srv.yaml(filename)-----service file
metadata:									kubectl apply -f platforms-depl.yaml(filename)-----deployment file
    name: commands-depl									same commands for deployment as well as service file..
spec:									---------------------------------------------------------------------------					
   replicas: 1								--------RESTART------
   selector:									kubectl rollout restart deployment platform-depl(DeploymentName||serviceName)
    matchLabels:							-------DELETE---------
        app: commandservice							kubectl delete platforms-np-srv (deploymentName||ServiceName)
   template:
     metadata:
        labels:
            app: commandservice
     spec:
        containers:
            - name : commandservice
              image: capitalmarkettec/commandsservice:latest
              ports: 
                - containerPort: 5000
---
apiVersion: v1
kind: Service
metadata:
    name: platforms-clusterip-srv
spec:
   type: ClusterIP
   selector:
    app: commandservice
   ports: 
   - name: commandservice
     protocol: TCP
     port: 4080
     targetPort: 5000
---------------------------------------------------------------
--------------------------------------------------------------- 	
--------------------------SERVICE---------------------------(EX)	
apiVersion: v1
kind: Service
metadata:
  name: platformnpservice-srv
spec:
  type: NodePort
  selector:
    app: platformservice
  ports:
    - name: platformservice
      protocol: TCP
      port: 4080
      targetPort: 5000

-----------------------------------------------------------------------
-----------------------------------------------------------------------
								
