## Jenkins tutorial for beginners

#### Let's get started !!

### Jenkins docker image

First, let us check the offical jenkins docker image from docker hub website [Docker Hub](https://hub.docker.com/search?q=jenkins)

As the Jenkins official Docker image is deprecated, we need to use the next docker image from the search list. This jenkins/jenkins image is maintained by Jenkins community and continuously updated.

<img width="1214" alt="image" src="https://user-images.githubusercontent.com/84066151/168812272-93ef9384-8d16-4364-8474-227ef813978b.png">

Direct link to jenkins docker image. [jenkins/jenkins](https://hub.docker.com/r/jenkins/jenkins)

### Start Jenkins Docker Container

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

### Verify Jenkins container status

Use ```docker ps``` command to list the running docker containers. If the container is not listed, use ```docker ps -a``` command to show all running and stopped containers.

```ruby

$ docker ps

CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                                             
cda0edfd1a30   jenkins/jenkins:lts   "/sbin/tini -- /usr/…"   11 minutes ago   Up 11 minutes   0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp

```

### Verify Jenkins container logs

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


### Login to Jenkins localhost

Let's open up the browser and type ```localhost:8080```. This is the port we exposed our jenkins container.

Copy and paste the password generated during jenkins initialization under Administrator password and click on continue. (Check out the previous step to copy password)

<img width="1150" alt="image" src="https://user-images.githubusercontent.com/84066151/168865737-8c99294f-21d0-4104-a89c-2369507ef4de.png">


###  Setup Jenkins [Getting Started]



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
