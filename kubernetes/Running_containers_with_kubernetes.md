# *Running Containers with Kubernetes*

situation-
Your company wants to spin up some application infrastructure on a new Kubernetes cluster. 
You have been given the task of setting up some basic containers and checking container 
logs to make sure everything is working properly.

You will need to run two containers in the cluster. One should run Nginx, and the other 
should run Redis. Then, check the logs of the Nginx container to make sure it is working 
as expected

run vi nginx-pod.yml
write yaml file with basic pod specs:
```

apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
    
```

<img width="554" alt="pod_one" src="https://user-images.githubusercontent.com/94250541/197270285-66286b0b-8038-4c1e-b2be-58567a5c22db.png">

<img width="554" alt="pod_two" src="https://user-images.githubusercontent.com/94250541/197270300-f6543de8-e7a1-4ce4-8aa1-c4a22af02034.png">

<img width="557" alt="pod_five" src="https://user-images.githubusercontent.com/94250541/197270392-1c929180-af60-428c-96ff-fdc9008b2493.png">

<img width="569" alt="pod_six" src="https://user-images.githubusercontent.com/94250541/197270410-37edb82f-4989-409d-9811-814bd7671665.png">

