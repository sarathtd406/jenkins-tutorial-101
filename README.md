## Jenkins tutorial for beginners

#### Let's get started !!

### Jenkins docker image

First, let us check the offical jenkins docker image from docker hub website [Docker Hub](https://hub.docker.com/search?q=jenkins)

As the Jenkins official Docker image is deprecated, we need to use the next docker image from the search list. This jenkins/jenkins image is maintained by Jenkins community and continuously updated.

<img width="1214" alt="image" src="https://user-images.githubusercontent.com/84066151/168812272-93ef9384-8d16-4364-8474-227ef813978b.png">

Direct link to jenkins docker image. [jenkins/jenkins](https://hub.docker.com/r/jenkins/jenkins)

### Start Docker Container

We can start Jenkins container using below command. Before that, **let's understand the command**.

1. The ```docker run``` command first creates a writeable container layer over the specified image, and then starts it using the specified command. <br></br>
2. We are exposing jenkins application to port 8080. Basically jenkins runs on tomcat which uses port 8080. Jenkins container also by default runs on port 8080. <br></br>
3. We are exposing another port 50000 which will used when we connect agents to the controller (Master/Slave communication). This will enable Jenkins to bind slaves incase if we add some in future. <br></br>
4. ```-d``` is an optional command used with ```docker run``` to run the container in background and print container ID. (Run in detach mode) <br></br>
5. ```-v``` is an optional command used with ```docker run``` to bind mount a volume to the container. Here we are using a named volume called ```jenkins_home``` which will be automatically created in your local machine. This ```jenkins_home``` directory is binded to ```/var/jenkins_home``` which resides inside jenkins container. This volumne mount is need to persit the data even when jenkins container gets restarted or deleted and recreated. <br></br>
6. Finally, docker image name that we are using. ```jenkins/jenkins:lts``` with latest tag. <br></br>


```
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

**reponse:**

```ruby

$ docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts

Unable to find image 'jenkins/jenkins:lts' locally
lts: Pulling from jenkins/jenkins
6aefca2dc61d: Pull complete 
e1108b695755: Pull complete 
4985c9eaee97: Pull complete 
8228d7831e76: Pull complete 
9519512ddfd4: Pull complete 
0733f6b69c1e: Pull complete 
b336c88402cb: Pull complete 
cb7dc9e53b9a: Pull complete 
e07562e27aae: Pull complete 
459456f5f3a7: Pull complete 
bba697df7a23: Pull complete 
fd343a6d7b0a: Pull complete 
064f97281dfa: Pull complete 
105e1c5c62b9: Pull complete 
47468e3b9259: Pull complete 
0c33547f2be5: Pull complete 
6ae3378125de: Pull complete 
Digest: sha256:3dec77ef6636c4f4068f855fb2857bd3e8942b12bdd9c7429bd64ab8bc392527
Status: Downloaded newer image for jenkins/jenkins:lts
cda0edfd1a300d9947e0a9369fc1317733f7f4324d1f27e1d4fc42e6b0d52167

```

### Verify container status

Use ```docker ps``` command to list the running docker containers. If the container is not listed, use ```docker ps -a``` command to show all running and stopped containers.

```ruby

$ docker ps

CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                                             
cda0edfd1a30   jenkins/jenkins:lts   "/sbin/tini -- /usr/…"   11 minutes ago   Up 11 minutes   0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp

```

### Verify container logs

Use ```docker logs <CONTAINER ID>``` command to fetch the logs of a container.

```ruby
$ docker logs cda0edfd1a30

Running from: /usr/share/jenkins/jenkins.war
webroot: EnvVars.masterEnvVars.get("JENKINS_HOME")

2022-05-17 16:23:16.507+0000 [id=35]	INFO	jenkins.install.SetupWizard#init: 

*************************************************************
*************************************************************
*************************************************************

Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

< password >

This may also be found at: /var/jenkins_home/secrets/initialAdminPassword

*************************************************************
*************************************************************
*************************************************************

2022-05-17 16:23:30.838+0000 [id=35]	INFO	jenkins.InitReactorRunner$1#onAttained: Completed initialization
2022-05-17 16:23:30.857+0000 [id=23]	INFO	hudson.lifecycle.Lifecycle#onReady: Jenkins is fully up and running
2022-05-17 16:23:31.919+0000 [id=49]	INFO	h.m.DownloadService$Downloadable#load: Obtained the updated data file for hudson.tasks.Maven.MavenInstaller
2022-05-17 16:23:31.921+0000 [id=49]	INFO	hudson.util.Retrier#start: Performed the action check updates server successfully at the attempt #1
2022-05-17 16:23:31.927+0000 [id=49]	INFO	hudson.model.AsyncPeriodicWork#lambda$doRun$1: Finished Download metadata. 15,993 ms

```

**Here in above logs you can see that jenkins has started and initialized successfully and generated a configuration password to proceed further.**


### Login to Jenkins

Let's open up the browser and type ```localhost:8080```. This is the port we exposed our jenkins container.

Copy and paste the password generated during jenkins initialization under Administrator password and click on continue. (Check out the previous step to copy password)

<img width="1150" alt="image" src="https://user-images.githubusercontent.com/84066151/168865737-8c99294f-21d0-4104-a89c-2369507ef4de.png">


###  Getting Started Jenkins

Now, we are in the Jenkins Getting Started page as shown below. Let's select **Install suggested plugins** by jenkins community. 

Even you can know the jenkins version mentioned at the bottom of this page. **Version - Jenkins 2.332.3**

<img width="1144" alt="image" src="https://user-images.githubusercontent.com/84066151/168869366-a98a7bc5-e7b7-4d7e-8d72-96ebb194b5cc.png">

**Wait until the plugins are installed. **

<img width="1177" alt="image" src="https://user-images.githubusercontent.com/84066151/168870697-e0ce6139-5ae4-4154-9776-2e4d9a379602.png">

We can install other plugins later as well.


### Create Admin user 

As shown in below image,

1. Enter username
2. Enter password
3. Enter full name
4. Enter email id

Click on **Save and Continue**

<img width="1155" alt="image" src="https://user-images.githubusercontent.com/84066151/168871607-3a951b2a-6f1b-4c3a-9efd-f7d1b3041498.png">


### Set Instance URL

Let us leave the default URL setting and click on **Save and Finish**

<img width="1133" alt="image" src="https://user-images.githubusercontent.com/84066151/168872166-615320ce-61db-41a7-8ef9-18a91b17ccf4.png">

### Ready to use

Click on **Start using Jenkins**

<img width="1157" alt="image" src="https://user-images.githubusercontent.com/84066151/168872400-fac7f418-b78f-4f8d-afe1-b1aaa9870859.png">


**Welcome to Jenkins**

<img width="1432" alt="image" src="https://user-images.githubusercontent.com/84066151/168872577-6dbdf5ef-f511-4828-b0fd-604bd408efb9.png">


### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/sarathtd406/jenkins-tutorial-101/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
