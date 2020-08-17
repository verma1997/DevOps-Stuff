# DevOps

# Jenkins Master-Slave Configuration
For configuring the master-slave configuration in jenkins,

### Step 1: Install the Kubernetes plugin
To install, navigate to **Manage Jenkins > Manage Plugins** then search for *Kubernetes Plugin*. This plugin integrate the Kubernetes with Jenkins<br />
![](images/k8s-plugin.png)<br />

### Step 2: Setup the Cloud for Kubernetes

*  Go to **Manage Jenkins > Configure System > Cloud** and click on **Add a new cloud** and select **Kubernetes** from there.<br />

![](images/master-slave-1.png)<br />

*  Click on **Kubernetes Cloud Details** to enter the necessary Kubernetes details.
```
    Kubernetes URL        -> 
    Kubernetes Namespace  -> 
    Jenkins URL           ->
```
![](images/k8s-details-1.png)<br />

**NOTE** For Kubernetes URL, use `$ kubectl config view | grep master` command.
*  Click on **Pod Template > Add Pod Template** and fill out the essentials details.
```
    Name        ->
    Namespace   ->
    Labels      ->
    Usage       ->
```
![](images/pod-1.png)<br />

*  Click on **Add Container** and fill out the necessary details.
```
    Name                                   -> jnlp
    Docker Image (Image of Jenkins-Agent)  -> gcr.io/<project_id>/jenkins-slave-tf:v1
    Working DIrectory                      -> /home/jenkins/agent
```
![](images/container-1.png)<br />

*  Also mount the **Host Path Volume**.

1st
```
    Host Path    -> /var/run/docker.sock
    Mount Path   -> /var/run/docker.sock
```

2nd
```
    Host Path    -> /tmp/
    Mount Path   -> /var/artifacts
```
![](images/volumes-1.png)<br />

*  Click on **Apply** and then **Save**.
