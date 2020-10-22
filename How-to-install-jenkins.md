# Jenkins

Here we will learn about Jenkins, why a DevOps engineer prefers Jenkins for CI/CD. Well, it is an open source continuous integration and continuous delivery (CI &CD) server with which organizations can automate their software development process. Jenkins does this by managing and controlling development lifecycle processes by breaking them up into Jenkins jobs. Jenkins has written in Java with plugins built for Continuous Integration purpose.

Step-1 Update your CentOS 7 system.

`sudo yum install epel-release
sudo yum update`

Step 2: Install Java.

before installing Jenkins you need to install java in your machine. let’s install the latest version of OpenJDK Runtime Environment 1.8.0
`sudo yum install java-1.8.0-openjdk.x86_64`

After installing Java you can verify it by running the flowing command.
`java -version
This command will let you know the runtime environment of the java version.

`openjdk version "1.8.0_91"
OpenJDK Runtime Environment (build 1.8.0_91-b14)
OpenJDK 64-Bit Server VM (build 25.91-b14, mixed mode)
`

Step 3: Install Jenkins.

Start by importing the repository key from Jenkins.
`sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
`
After importing the key, add the repository to the system.

`sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
`
Now install the Jenkins package using yum:
`sudo yum install jenkins
`

You can now start Jenkins service using:

`sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins`

Enable port 8080/tcp on the firewall.

`sudo firewall-cmd --add-port=8080/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
`

Service should be listening on port 8080:

`netstat -tunelp | grep 8080
tcp    LISTEN     0      50       :::8080                 :::*`

Unblocking Jenkins

Browse to the URL http://[serverip|hostname]:8080 to access the web installation wizard.
When you first access a new Jenkins instance, you are asked to unlock it using an automatically generated password.

The admin password is created and stored in the log file “/var/log/jenkins/jenkins.log“. Run the below command to get the password.

`sudo grep -A 5 password /var/log/jenkins/jenkins.log`


