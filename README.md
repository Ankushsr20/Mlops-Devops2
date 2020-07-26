# Mlops-Devops2
In this project, we can see the integration of Jenkins, Docker, Git, and GitHub with the help of the following objectives:
 -Create a Docker container image that has Jenkins installed using Dockerfile. When we launch this image, it should automatically start the Jenkins service in the container.
 -Create a job chain of job1, job2, job3, and job4 using the build pipeline plugin in Jenkins.

Now, before we go into details regarding the jenkins jobs, our first objective is to create all the container images that can come into use for us. Currently, the type of code files I am considering are HTML (.html), (.php), and Python (.py) files. Hence, we need to create four Dockerfile for launching Jenkins, HTML, and Python files each.

There are multiple methods to create custom Docker container images, but the method we will use is the creation of Dockerfiles. To create a Dockerfile, we first need to set up a workspace from the command line. After that we need to create a Dockerfile using the `gedit Dockerfile` command.
![2](https://user-images.githubusercontent.com/64484790/88488529-59225180-cfab-11ea-9561-30ee76204a5b.jpg)

1. `FROM centos` - It references the base OS for the new image.
2. `RUN yum install wget -y` - Installation of wget command (Used to install Jenkins)
3. `RUN yum install net-tools -y` - Installation of net-tools which form the base of Linux OS networking
4. `RUN wget -0 /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo`
5. `RUN rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key` - Commands 4. and 5. are meant for the installation of Jenkins. (Refer to the link https://www.jenkins.io/download/ )
6. `RUN yum install java -y && yum install jenkins -y` - The installation of Jenkins and Java as Jenkins is dependant on Java for its working.
7. `RUN yum install git -y` - Installation of Git to perform commands by interacting with GitHub repositories
8. `RUN yum install gedit -y` - Installation of text editor Gedit for performing minor changes in the configuration files of Jenkins to enable email services. (Optional)
9. `RUN yum install openssh-clients -y` — The installation allows us to use remote access of other systems from within the container and vice-versa.
10. `RUN echo -e "jenkins ALL=(ALL) NOPASSWD:ALL" /etc/sudoers` - This allows Jenkins to have maximum access to perform commands by modifying the sudoers file.

![1](https://user-images.githubusercontent.com/64484790/88488787-2b3e0c80-cfad-11ea-82a7-748b24a06191.jpg)

Now let us start building the jobs.

# Job1 - Pulling the Github Repository once commit is made
We can do this using the jenkins job and creating hooks using post-commit.sample file for this part refer to my previous project for more details. First job is configured as follows.

![3](https://user-images.githubusercontent.com/64484790/88488832-a30c3700-cfad-11ea-9fbc-d25cad2834b4.jpg)

# Job2- By looking at the file pushed by developer job2 will automatically create a web server

Also, the job2 will be started as soon as job1 is completed as job1 is set as upstream project of job2

![5](https://user-images.githubusercontent.com/64484790/88488867-05fdce00-cfae-11ea-893f-45f629ccd050.jpg)

# Job3- This will test the server and if server works properly then the code will exit if server is not working then the build will fail and will send the details to our mail id.

![6](https://user-images.githubusercontent.com/64484790/88488884-37769980-cfae-11ea-9870-3a722fd76f6d.jpg)

![7](https://user-images.githubusercontent.com/64484790/88488904-537a3b00-cfae-11ea-9b1d-ae4a7bfe5d50.jpg)

# Job4-This build will check periodically if the container is working or not if not then it will deploy a new container automatically

![8](https://user-images.githubusercontent.com/64484790/88488932-7e648f00-cfae-11ea-912a-679fa3d6b4ca.jpg)

![9](https://user-images.githubusercontent.com/64484790/88488939-8c1a1480-cfae-11ea-832b-7a10ed47f0c1.jpg)

# We now create a Build Pipeline - It is a interactive way of using and managing jenkins and jobs. It is a powerful feature in which a large builds can be managed and visualised easily

![4](https://user-images.githubusercontent.com/64484790/88488945-96d4a980-cfae-11ea-9bb8-e89112eccc81.jpg)

Thank you!
