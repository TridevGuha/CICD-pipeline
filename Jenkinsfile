pipeline{
    agent any
    stages{
        stage('git'){
            steps{
                git 'https://github.com/coolgourav147/spring-boot-war-example.git' // this also cleans existing same git folder
            }
        }
        stage('test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('build'){
            steps{
                sh 'mvn install'
                sh 'mv target/hello-world-*.war target/app.war'
            }
        }
        stage('deploy'){
          steps{
            sshagent(['tomcat']) {
                 sh 'scp -o StrictHostKeyChecking=no target/app.war root@tomcat:/var/lib/tomcat9/webapps/'   
         
             }
          }
        }   
    }
}

/*
================
for mvn commands to run:
1. install mvn with apt. No need to install maven with jenkins global installer.

for stage('deploy') to run successfully, preconfigurations at server:
1. change hostname of both servers. jenkins , tomcat
2. make JENKINS ALL(ALL:ALL) ALL entry in /etc/sudoers file.
3. make ssh passwordless between: jenkins instance's jenkins user -and/to- tomcat instance's root user(ref: scp root@tomcat)
================
*/
