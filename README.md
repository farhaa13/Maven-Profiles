# Maven-Profiles
Profile is used to create a portable builds

# ETOE Maven Profiles Project
This project demonstrates how to deploy a Java web application to multiple environments (Dev, QA, Prod) using Maven profiles.
## Architecture

Code → Maven → Profile → Tomcat → Deployment
## Maven Profiles

| Environment | Profile | Port |
|------------|--------|------|
| Dev        | dev    | 8080 |
| QA         | qa     | 8085 |
| Prod       | prod   | 8090 |
## Steps to Run the Project
### 1. Launch 3 instances for Dev,Prod,QA 
server with differenet security groups

### 2. Install java & tomcat in all three servers
Inside cd/opt/ directory
`yum install java-17*`
`wget https://archive.apache.org/dist/tomcat/tomcat-7/v7.0.93/bin/apache-tomcat-7.0.93.tar.gz`

### 3. Install maven in devserver only
`https://dlcdn.apache.org/maven/maven-3/3.9.14/binaries/apache-maven-3.9.14-bin.tar.gz`

### 4. Set path of java & maven in ~/.bash_profile
[export JAVA_HOME=/usr/lib/jvm/java-17-amazon-corretto.x86_64
export M2_HOME=/opt/maven
export PATH=$JAVA_HOME/bin:$M2_HOME/bin:$PATH]

### 5. Save the changes permanantly
`source ~/.bash_profile`

### 6. Add user detail in tomcat-users.xml in all three servers
[<role rolename="manager-gui"/>
 <role rolename="manager-script"/>
 <role rolename="manager-jmx"/>
 <role rolename="manager-status"/>
 <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>]
 
### 7. Edit server.xml of tomcat
add port according to your servers inside the connector port section 

### 8. Insatll git on devserver only
`yum install git`

### 9. Clone the Repository
git clone https://github.com/farhaa13/etoe.git

### 10. Navigate to Project
cd etoe

### 11. Edit the pom.xml file
add build profiles for Dev,QA,Prod environment

### 12. Check the syntax error 
`mvn validate`

### 13. Build the Project
`mvn clean package`

### 14. Deploy to Dev
`mvn tomcat7:deploy -Pdev`
![dev-deploy](https://github.com/user-attachments/assets/c55b4920-5876-485f-be80-1a0aa5a505e5)

### 5. Deploy to QA
`mvn tomcat7:deploy -Pqa`
![QA-deploy](https://github.com/user-attachments/assets/d4f691fa-9c53-44a6-9b2f-a85aaf74de3c)

### 6. Deploy to Prod
`mvn tomcat7:deploy -Pprod`
![Prod-deploy](https://github.com/user-attachments/assets/ec305b1b-8941-45e9-9126-825e85468a46)




