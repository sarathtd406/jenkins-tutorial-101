## Jenkins tutorial for beginners

#### Let's get started !!

### Jenkins docker image

First, let us check the offical jenkins docker image from docker hub website [Docker Hub](https://hub.docker.com/search?q=jenkins)

As the Jenkins official Docker image is deprecated, we need to use the next docker image from the search list. This jenkins/jenkins image is maintained by Jenkins community and continuously updated.

<img width="1214" alt="image" src="https://user-images.githubusercontent.com/84066151/168812272-93ef9384-8d16-4364-8474-227ef813978b.png">

Direct link to jenkins docker image. [jenkins/jenkins](https://hub.docker.com/r/jenkins/jenkins)

### Start Jenkins Docker Container

We can start Jenkins container using below command. Before that, let's understand the command.

1. The ```docker run``` command first creates a writeable container layer over the specified image, and then starts it using the specified command. <br></br>
2. We are exposing jenkins application to port 8080. Basically jenkins runs on tomcat which uses port 8080. Jenkins container also by default runs on port 8080. <br></br>
3. We are exposing another port 50000 which will used when we connect agents to the controller (Master/Slave communication). This will enable Jenkins to bind slaves incase if we add some in future. <br></br>
4. ```-d``` is an optional command used with ```docker run``` to run the container in background and print container ID. (Run in detach mode) <br></br>
5. ```-v``` is an optional command used with ```docker run``` to bind mount a volume to the container. Here we are using a named volume called ```jenkins_home``` which will be automatically created in your local machine. This ```jenkins_home``` directory is binded to ```/var/jenkins_home``` which resides inside jenkins container. This volumne mount is need to persit the data even when jenkins container gets restarted or deleted and recreated. <br></br>
6. Finally, docker image name that we are using. ```jenkins/jenkins:lts``` with latest tag. <br></br>


```
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```


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
