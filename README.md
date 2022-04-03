# Comodo_Devops_Pipeline_simple_app

This repository is for the
[Build a Java app with Maven](https://jenkins.io/doc/tutorials/build-a-java-app-with-maven/)
tutorial in the [Jenkins User Documentation](https://jenkins.io/doc/).

The repository contains a simple Java application which outputs the string
"Hello world!" and is accompanied by a couple of unit tests to check that the
main application works as expected. The results of these tests are saved to a
JUnit XML report.

The `jenkins` directory contains an example of the `Jenkinsfile` (i.e. Pipeline)
you'll be creating yourself during the tutorial and the `scripts` subdirectory
contains a shell script with commands that are executed when Jenkins processes
the "Deliver" stage of your Pipeline.

$sudo update-alternatives --config java

## JAVA 8 installation in ubuntu 16.04

- sudo apt-get -y install default-jdk

## JAVA 8 installation in ubuntu 18.04

- sudo apt update
- sudo apt install openjdk-8-jdk openjdk-8-jre
- set path 
```
cat >> /etc/environment <<EOL
JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
JRE_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre
EOL
```

execute command - sudo update-alternatives --config java ( select which ever java version you need )

## Java 11 ( open JDK )
- sudo add-apt-repository ppa:openjdk-r/ppa
- sudo apt-get update
- sudo apt install openjdk-11-jdk


## JAVA 11 installation in ubuntu 16.04

 - sudo add-apt-repository ppa:linuxuprising/java
 - sudo apt update
 - sudo apt-get install oracle-java11-installer
 - sudo apt-get install oracle-java11-set-default ( to set java 11 as default ) 
 - java -version ( verify java installation )

## JAVA 11 installation in ubuntu 18.04


for more details - https://tecadmin.net/install-oracle-java-11-on-ubuntu-16-04-xenial/

#### JAVA 11 installation in GCP machine 
  - download **jdk-11.0.12_linux-x64_bin.tar.gz** from https://www.oracle.com/java/technologies/downloads/#java11 and place it under **/var/cache/oracle-jdk11-installer-local**
  - sudo apt-get install oracle-java11-installer-local
  - sudo apt install oracle-java11-set-default-local




## git installation in ubuntu 16.04
 
 - apt-get update
 - apt-get install git
 - git --version ( to verify git version )
 

## Jenkins installation in ubuntu 16.04
 
 - wget https://updates.jenkins-ci.org/download/war/2.162/jenkins.war ( installs 2.162 version, if you want any other version to be installed visit https://updates.jenkins-ci.org/download/war/ download particular version )
 - wget https://updates.jenkins-ci.org/download/war/2.303.2/jenkins.war
- java -jar jenkins.war ( default runs on 8080 port ) 
 - java -jar jenkins.war --httpPort=5000 ( if you want run on any other port use this, in my case its 5000 port ) 
 - nohup java -jar jenkins.jar & ( to run jenkins process in background )
 
## Jenkins as a service 
 - wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
 - echo deb https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list
 - apt-get update
 - apt-get install jenkins
 - systemctl start jenkins
 - systemctl status jenkins
 
   
## maven installation in ubuntu 16.04 
 
 -  cd /usr/local
 - wget https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
 - sudo tar xvf apache-maven-3.6.3-bin.tar.gz 
 - ln -s apache-maven-3.6.3 apache-maven
 - sudo vi /etc/profile.d/apache-maven.sh
 
        please insert below lines to /etc/profile.d/apache-maven.sh
        
          export JAVA_HOME=/usr/lib/jvm/java-11-oracle
          export M2_HOME=/usr/local/apache-maven
          export MAVEN_HOME=/usr/local/apache-maven
          export PATH=${M2_HOME}/bin:${PATH}
   
 - source /etc/profile.d/apache-maven.sh
 - mvn -version ( to verify maven version ) 
 
 For more details https://tecadmin.net/install-apache-maven-on-ubuntu/ 
 
 easy way to install - sudo apt install maven
 
   
 ## Docker installation in ubuntu 16.04
 
 - sudo apt-get update
 - sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
 - curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
 - sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
 - sudo apt-key fingerprint 0EBFCD88
 - sudo apt-get update
 - sudo apt-get install docker-ce docker-ce-cli containerd.io ( to install latest version )
 - sudo docker run hello-world

if you want all the things in a script use https://github.com/DeekshithSN/cheatsheet/blob/master/docker-install.sh

for more details refer  https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce-1 

        If you face below problem which is same as mentione below the you can refer this link

       https://stackoverflow.com/questions/25183063/docker-on-rhel-6-cgroup-mounting-failing

       Starting cgconfig service: Error: cannot create directory /cgroup/blkio
        /sbin/cgconfigparser; error loading /etc/cgconfig.conf: Cgroup, operation not allowed
       Failed to parse /etc/cgconfig.conf                         [FAILED]

       After doing this you need run all the commands with sudo concatenated to it.

        - To solve this issue we need to add current user to docker group , to do the same follow the below commands 
          sudo groupadd docker
          sudo usermod -aG docker $USER ( got a error while runing docker commands with the current user)
          sudo usermod -aG docker jenkins (got a error while runing docker commands with jenkins user )
          getent group <groupname> (to check the list of users in particular group)
          sudo passwd jenkins to change password of jenkins user
        
        - even after following the above commands if you face any issue in ruuning commands then run below command
          chmod 777 /var/run/docker.sock
        
## SonarQube Installation in ubuntu 16.04 

Use apt-get to install the required packages.
 - apt-get update
 - apt-get install unzip software-properties-common wget default-jdk
 
Install the PostgreSQL database service.
 - apt-get install postgresql postgresql-contrib
 
Access the Postgres database service command-line.
 - su - postgres
 - psql
 
Create a Postgres user named sonarqube,Create a Postgres database named sonarqube.
Give the PostgreSQL user named sonarqube permission over the database named sonarqube
 - CREATE USER sonarqube WITH PASSWORD 'password';
 - CREATE DATABASE sonarqube OWNER sonarqube;
 - GRANT ALL PRIVILEGES ON DATABASE sonarqube TO sonarqube;
 - \q
 
Download the Sonarqube package and move it to the OPT directory.
 - mkdir /downloads/sonarqube -p
 - cd /downloads/sonarqube
 - wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.9.1.zip
 - unzip sonarqube-7.9.1.zip
 - mv sonarqube-7.9.1 /opt/sonarqube
 
Create a new Linux account named sonarqube, Set the correct file permission on the sonarqube directory.
 - adduser --system --no-create-home --group --disabled-login sonarqube
 - chown -R sonarqube:sonarqube /opt/sonarqube
 
Edit the sonar.sh configuration file.
 - vi /opt/sonarqube/bin/linux-x86-64/sonar.sh
 
Configure the following options:
 - RUN_AS_USER=sonarqube
 
Edit the sonar.properties configuration file.
 - vi /opt/sonarqube/conf/sonar.properties
 
Configure the following options:

      sonar.jdbc.username=sonarqube
      sonar.jdbc.password=password
      sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube
      sonar.web.javaAdditionalOpts=-server
      sonar.web.host=0.0.0.0
		
Create a Linux configuration file named 99-sonarqube.conf
 - vi /etc/security/limits.d/99-sonarqube.conf
 
Here  is the content of the 99-sonarqube.conf file.
		
    sonarqube   -   nofile   65536
    sonarqube   -   nproc    4096

Edit the sysctl.conf configuration file.
 - vi /etc/sysctl.conf
 
Add the following lines at the end of the sysctl.conf file.

      vm.max_map_count=262144
      fs.file-max=65536

Reboot your computer to enable the new configuration
 - reboot
 
Start the Sonarqube service.
 - /opt/sonarqube/bin/linux-x86-64/sonar.sh start
 
Use the following command to monitor the SonarQube log.
 -  tail -f /opt/sonarqube/logs/sonar.log

for more deatils refer - https://techexpert.tips/sonarqube/sonarqube-installation-ubuntu-linux/

#### you want to create sonarqube through docker then use below command 

```
docker run -d -p 9000:9000 sonarqube:lts
```

## JFROG Artifactory installation in ubuntu 16.04 using docker container 

 - export JFROG_HOME= /set/some/path
 - mkdir -p $JFROG_HOME/artifactory/var/etc/
 - cd $JFROG_HOME/artifactory/var/etc/
 - touch ./system.yaml
 - chown -R 1030:1030 $JFROG_HOME/artifactory/var
   
   run below docker command 

      docker run --name artifactory -v $JFROG_HOME/artifactory/var/:/var/opt/jfrog/artifactory -d -p 8081:8081 -p 8082:8082 docker.bintray.io/jfrog/artifactory-oss:latest
   
   
## Ansible Installation in ubuntu 16.04

 - sudo apt-add-repository ppa:ansible/ansible
 - sudo apt-get update
 - sudo apt-get install ansible

For more details - https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-16-04


## kubernetes installation on ubuntu 16.04 ( kubeadm - single master multi nodes )

Make sure docker installed in master and nodes, make sure master has 2 cpu's 

Execute below commands in both master and node 

 - sudo apt-get update && sudo apt-get install -y apt-transport-https curl
 - curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
 - cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list <br />
   deb https://apt.kubernetes.io/ kubernetes-xenial main <br />
   EOF
 - sudo apt-get update
 - sudo apt-get install -y kubelet kubeadm kubectl
 - sudo apt-mark hold kubelet kubeadm kubectl

for more details https://kubernetes.io/docs/setup/independent/install-kubeadm/

Execute below commands in master 

after executing this command you will get node's joining command, copy and paste it somewhere 
 - kubeadm init --pod-network-cidr=10.244.0.0/16 ( if you have forget to do then use kubeadm token create --print-join-command ) 
 - export KUBECONFIG=/etc/kubernetes/admin.conf
 - mkdir -p $HOME/.kube
 - sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
 - sudo chown $(id -u):$(id -g) $HOME/.kube/config;mkdir -p $HOME/.kube
 - sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
 - kubectl apply -f https://docs.projectcalico.org/v3.3/getting-started/kubernetes/installation/hosted/canal/rbac.yaml
 - kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/2140ac876ef134e0ed5af15c65e414cf26827915/Documentation/kube-flannel.yml

Execute join command in node, which may look like as mentioned below 

       kubeadm join 10.128.0.8:6443 --token q915fe.do2ty6a8ow6qjixt \
       --discovery-token-ca-cert-hash sha256:acd137106e6b763d1ca6b5a4f7c1b1538c2ee8af81e47f9ea3f385c66cd710b3 

Then to verify use below commands
 - kubectl get nodes
 - kubectl get pods
 - Kubectl get service
 
 ## Nexus Installation in ubuntu 16.04

 - apt-get install wget ( install if you dont have wget )
 - java -version ( make sure java is installed which should be java 8 or higher version )
 - wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz 
 - tar -xvf latest-unix.tar.gz  
 - cd nexus-3.35.0-02/bin
 - ./nexus start ( starts the nexus artifactory )
 - ./nexus status ( by this you check the status of nexus artifactory )
 - To access this use http://ip_Address:8081 ( by deafault which will be running on 8081)
 
  ``` intial password will be present in /opt/sonatype-work/nexus3/admin.password ```
  
 ## Helm Installation in ubuntu 16.04
 
 - curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
 - chmod 700 get_helm.sh 
 - ./get_helm.sh
 
 	### helm uninstallation 
	- which helm ( to see which folder its installed )
	- rm -rf /usr/local/bin/helm


## installing kubeadm on GCP machines

#### Install kubelet, kubeadm and kubectl

add Kubernetes repository for Ubuntu 20.04 to all the servers.
```
sudo apt update
sudo apt -y install curl apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
Then install required packages.

```
sudo apt update
sudo apt -y install vim git curl wget kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

Confirm installation by checking the version of kubectl.

```
kubectl version --client && kubeadm version
```
```
Client Version: version.Info{Major:"1", Minor:"22", GitVersion:"v1.22.2", GitCommit:"8b5a19147530eaac9476b0ab82980b4088bbc1b2", GitTreeState:"clean", BuildDate:"2021-09-15T21:38:50Z", GoVersion:"go1.16.8", Compiler:"gc", Platform:"linux/amd64"}
kubeadm version: &version.Info{Major:"1", Minor:"22", GitVersion:"v1.22.2", GitCommit:"8b5a19147530eaac9476b0ab82980b4088bbc1b2", GitTreeState:"clean", BuildDate:"2021-09-15T21:37:34Z", GoVersion:"go1.16.8", Compiler:"gc", Platform:"linux/amd64"}

```
#### Disable Swap


Turn off swap.
```
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
sudo swapoff -a
```
Enable kernel modules and configure sysctl.

Enable kernel modules
```
sudo modprobe overlay
sudo modprobe br_netfilter
```

 Add some settings to sysctl
 ```
sudo tee /etc/sysctl.d/kubernetes.conf<<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
EOF
```

Reload sysctl
```
sudo sysctl --system
```
#### Install Container runtime

##### Installing Docker runtime:

 Add repo and Install packages
 ```
sudo apt update
sudo apt install -y curl gnupg2 software-properties-common apt-transport-https ca-certificates
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y containerd.io docker-ce docker-ce-cli

sudo apt-get install -y docker.io
```

##### Create required directories
```
sudo mkdir -p /etc/systemd/system/docker.service.d
```

##### Create daemon json config file
```
sudo tee /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
```

##### Start and enable Services
```
sudo systemctl daemon-reload 
sudo systemctl restart docker
sudo systemctl enable docker
```

##### Ensure you load modules
```
sudo modprobe overlay
sudo modprobe br_netfilter
```

##### Set up required sysctl params
```
sudo tee /etc/sysctl.d/kubernetes.conf<<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
EOF
```

##### Reload sysctl
```
sudo sysctl --system
```

#### Initialize master node

Login to the server to be used as master and make sure that the br_netfilter module is loaded:

```
lsmod | grep br_netfilter
```

Enable kubelet service.

```
sudo systemctl enable kubelet
```

Initialize kubeadm 
```
kubeadm init
```

Configure kubectl using commands in the output:
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

//Check in master 
root@master-1:/home/mesomofficial# kubectl get nodes
NAME       STATUS     ROLES                  AGE    VERSION
master-1   NotReady   control-plane,master   84m    v1.23.5


Additional nodes can be added using the command in installation output:
```
kubeadm join 10.182.0.3:6443 --token 1rniu3.zytr9rvu4fbxqixt \
        --discovery-token-ca-cert-hash sha256:f500eb03acd261b64539c54da0be49907c399eebcd3b9371fbedf9608048095e



```
//Node is added and linked after the upper command 

root@master-1:/home/mesomofficial# kubectl get nodes
NAME       STATUS     ROLES                  AGE    VERSION
master-1   NotReady   control-plane,master   84m    v1.23.5
node-1     NotReady   <none>                 105s   v1.23.5


##Check all the nodes 
kubectl get nodes
    
 ### Install network plugin on Master

In this we’ll use Calico. You can choose any other supported network plugins.
```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml


```

After this 

My node is ready 

root@master-1:/home/mesomofficial# kubectl get nodes
NAME       STATUS   ROLES                  AGE    VERSION
master-1   Ready    control-plane,master   84m    v1.23.5
node-1     Ready    <none>                 113s   v1.23.5


root@master-1:/home/mesomofficial# kubectl get po --all-namespaces
NAMESPACE     NAME                                       READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-56fcbf9d6b-mxj7q   1/1     Running   0          6m33s
kube-system   calico-node-9gnc7                          1/1     Running   0          6m33s
kube-system   calico-node-zwdqw                          1/1     Running   0          6m33s
kube-system   coredns-64897985d-8h2fz                    1/1     Running   0          90m
kube-system   coredns-64897985d-zm6gn                    1/1     Running   0          90m
kube-system   etcd-master-1                              1/1     Running   0          90m
kube-system   kube-apiserver-master-1                    1/1     Running   0          90m
kube-system   kube-controller-manager-master-1           1/1     Running   0          90m
kube-system   kube-proxy-58jv6                           1/1     Running   0          90m
kube-system   kube-proxy-cltj5                           1/1     Running   0          8m1s
kube-system   kube-scheduler-master-1                    1/1     Running   0          90m
root@master-1:/home/mesomofficial# 






==============came to jenkins server and install these files ======================================


install Helm in jenkins server 


## Helm Installation in ubuntu 18.04
 
 - curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
 - chmod 700 get_helm.sh 
 - ./get_helm.sh
 
 	### helm uninstallation 
	- which helm ( to see which folder its installed )
	- rm -rf /usr/local/bin/helm

## Docker install in jenkins

sudo apt update
sudo apt install -y curl gnupg2 software-properties-common apt-transport-https ca-certificates
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y containerd.io docker-ce docker-ce-cli   //not working try below command

sudo apt-get install -y docker.io



//you can write a .sh like below and run it like $ sudo sh docker.sh  // it will install alll the files one by one 

=================
##Docker.sh

sudo apt-get update -y
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-key fingerprint 0EBFCD88
sudo apt-get update -y
sudo apt-get install -y docker.io

===============


sudo apt-get install -y unzip


====

Integration of datree in helm , so that we coulld know what will be the configuration error in future //more details https://hub.datree.io/

helm plugin install https://github.com/datreeio/helm-datree


=========================================================================
##setup Sonar cube 


log in to sonar server 

sudo apt-get update -y
root@sonar-1:/home/mesomofficial# sudo vi /etc/apt/sources.list

add this line in last line //deb [trusted=yes] http://downloads.sourceforge.net/project/sonar-pkg/deb binary/

sudo apt-get update -y

sudo apt install sonar -y 


root@sonar:/home/mesomofficial# sudo systemctl status
● sonar
    State: running
     Jobs: 0 queued
   Failed: 0 units
    Since: Thu 2022-03-31 05:52:31 UTC; 6h ago
   CGroup: /
           ├─1074 bpfilter_umh
           ├─user.slice
           │ └─user-1001.slice
           │   ├─session-11.scope
           │   │ ├─ 6931 sshd: mesomofficial [priv]
           │   │ ├─ 7061 sshd: mesomofficial@pts/0
           │   │ ├─ 7076 -bash
           │   │ ├─ 7189 sudo su
           │   │ ├─ 7191 su
           │   │ ├─ 7192 bash
           │   │ ├─10673 sudo systemctl status
           │   │ └─10674 systemctl status
           │   └─user@1001.service
           │     └─init.scope
           │       ├─6942 /lib/systemd/systemd --user
           │       └─6943 (sd-pam)
           ├─init.scope
           │ └─1 /sbin/init
           └─system.slice
             ├─systemd-networkd.service
             │ └─831 /lib/systemd/systemd-networkd
             ├─systemd-udevd.service
             │ └─477 /lib/systemd/systemd-udevd
             ├─google-osconfig-agent.service
             │ └─1082 /usr/bin/google_osconfig_agent
lines 1-31


//start the sonar service 

root@sonar:/home/mesomofficial# sudo systemctl start sonar 
root@sonar:/home/mesomofficial# sudo systemctl status sonar
● sonar.service - LSB: Sonar
   Loaded: loaded (/etc/init.d/sonar; generated)
   Active: active (exited) since Thu 2022-03-31 12:40:02 UTC; 5s ago
     Docs: man:systemd-sysv-generator(8)
  Process: 10817 ExecStart=/etc/init.d/sonar start (code=exited, status=0/SUCCESS)

Mar 31 12:40:01 sonar systemd[1]: Starting LSB: Sonar...
Mar 31 12:40:01 sonar su[10820]: Successful su for sonar by root
Mar 31 12:40:01 sonar su[10820]: + ??? root:sonar
Mar 31 12:40:01 sonar su[10820]: pam_unix(su:session): session opened for user sonar by (uid=0)
Mar 31 12:40:01 sonar sonar[10817]: Starting SonarQube...
Mar 31 12:40:02 sonar sonar[10817]: Started SonarQube.
Mar 31 12:40:02 sonar su[10820]: pam_unix(su:session): session closed for user sonar
Mar 31 12:40:02 sonar systemd[1]: Started LSB: Sonar.
root@sonar:/home/mesomofficial# 



error file in 
/opt/sonar/logs/sonar.log

that is java error 

root@sonar:/opt/sonar/logs# $sudo update-alternatives --config java
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
  0            /usr/lib/jvm/java-17-openjdk-amd64/bin/java      1711      auto mode
  1            /usr/lib/jvm/java-17-openjdk-amd64/bin/java      1711      manual mode
* 2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

Press <enter> to keep the current choice[*], or type selection number: 


reset ted the VM 

trying again .......




Jenkins

Admin
Som801886





## uncheck lightweight checkout  



this is the error you will face while pulling the master brach in jenkins


##jenkins with git

ssh -keygen
cat ~/.ssh/id_rsa.pub


ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCtlM2ADLEMAeuA1Q1p8Xq0Nlcc24FJJDm95u/TSyIGIv1VXtKCiF284vaQ0lc2RsqebCtk1TBbb1wFen8k5K2lteUmimqTnRBZg8LrNjP2/At8SdffNvzb1Sjhr9mdB4PpA9QVlzzGmmf+RLufh/p8rwhxBMiAqfqpjy5iAB1tcNXXltzEa3cMoVZ/q48CEQ2l1uRlnTDVYuCzSMmytB05U0P8flmfDuaoafTarXj59tIQpns8LxEqUMlAjpq3I91GxBd2ixGU0cAYTPaPq+3/vvXenCkYpI0bCQTSn0OrHhTweWgqD30DwA05rEZrnoHqoYYrSyW0BxiXaaLxfMLZ mesomofficial@jenkins



mesomofficial@jenkins:~/.ssh$ cat ~/.ssh/id_rsa
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEArZTNgAyxDAHrgNUNafF6tDZXHNuBSSQ5vebv00siBiL9VV7S
gohdvOL2kNJXNkbKnmwrZNUwW29cBXp/JOStpbXlJopqk50QWYPC6zYz9vwLfEnX
3zb829Uo4a/ZnQeD6QPUFZc8xppn/kS7n4f6fK8IcQTIgKn6qY8uYgAdbXDV15bc
xGt3DKFWf6uPAhENpdbkZZ0w1WLgs0jJsrQdOVND/H5Znw7mqGn02q14+fbSEKZ7
PC8RKlDJQI6atyPdRsQXdosRlNHAGEz2j6vt/7713pwpGKSNGwkE0p9Dqx4U8Hlo
Kg99A8ANOaxGa56B6qGGK0sltAcYl2mi8XzC2QIDAQABAoIBABD+UGAI3gxe479p
HDcS/QBHkZ+xnaabdUuyICh/YoVXR5XkApfk4chsL9ddwEwAAjYgQN9OP72z2T5w
D6J9AMMIW7a6NlTdO4yH6b09QTkc08MHN6sSpw6ef7IYlSVaZv+Y8Fpsw/Zth2DN
OdEUbuFmAV2PKlHuUivnaJMPj9H24K8OU4f+Co9Wnh0OjczconFraQ7Vjt7f7HyR
CluZl56NhrgnVjKN34oAEyOHyfZbmUVvYRMSIkNjSkMFgi1RWYAUWRgJ+nDKZDxw
TuouWiTlYjfub/znrsXhgCjDV/OWO5Xr00i+gvkxTl6bhlbzCBor9Tx4y8YZIf9a
VroefkECgYEA1/txDF3ChICHEN7lJHwCVatZ18Gqciu1i4xmPew6CByrFnJMkWAB
oagEu1eD0dMJN/5kGW1ObZzcI1pvtOx6GGm1xWa+66mw/WQmu/g/isUCNrIbFM/D
vpAG0CD7ZRxvnqMUzIuwwfYtykCPYDddHVVEh/bVihWj9Mq7F8skgEsCgYEAzb4u
pgOlA+OEWUWdw3HZwkVEc6cyCdFOZUCFEA8Y6qb8PKKICFSYW6uAyklFNFAz11Ed
u7muoWrCoIozHn8w1q6Jzg5l55BIJBtjs3hAKkgpoUanEUdLl7zLD+U2CQ3L3Jm0
rfM0xFJZJFVJY975SoU9vBzqvsZpM2vKZAd+OusCgYAytzNDgRy0+m080+ogmBIA
Rd0x4aMBbiwSGaTEc5zo3Lp76dj65f1cFVUPHKyyb4iholWk9trMuGGk146VgFXn
N6NcOBUqx0ztI0BJMTDSiBJN/6KGT4caTz2aT7RYeMXpDUhMA5083m7AKErCgB2Y
TrZp6tcXtp8qUxR9sNDgYwKBgQCaFPkomYgmnmiK1uks6wHTTT7Tgn6l/ZvBlo1Q
lo3phj9XRb2sx3YHCSz90dvDLuF0OqqS4Z+YAbVat8VK7KRt0u8fY4cL4fE1IVIM
oV0kjUCoKJqMBSHmtJw6/kT2iN+JCY/XylFVSfq6jCjXY7C9D4ZJcDqZv0wgF3TO
bxIpGwKBgQDILnMe6Lh1Mh7ceQSR2llx22lSklPUuAvxVW65PqOCW3MMWWZxszhW
JHY2dcGX0aXAWuLAIFTmV05O9DhWNJazmo85uIayjceMOAvauB9Xj+K0Jp3sazo6
Cihe2UsF9y2l6UxkJP+iwwYqVl+pb7bW5b7l45dxhec0IkGcLFEkqw==
-----END RSA PRIVATE KEY-----






## MAIN JENKINS CONFIGURATION ## VERY VERY IMP


give the path to main instead of master .... bydeafult in jenkins its master 



##install maven in jenkins server 

sudo apt update 

sudo apt install maven  


mvn --version 




set java path in mvn enviornment 



/usr/lib/jvm/java-1.8.0-openjdk-amd64

guide : https://www.youtube.com/watch?v=W-tVeRYTU2s&list=PLdsu0umqbb8PPKI5KQtWMeGv08d_aRmcp&index=2



root@jenkins:/home/mesomofficial# docker login -u admin -p Nexus@123 34.125.158.228:8083
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
root@jenkins:/home/mesomofficial# 
	
	
	
## Dockerhub account info 

![image](https://user-images.githubusercontent.com/17470074/161412775-f785e13a-ed04-4336-9de1-86473d96f12d.png)

