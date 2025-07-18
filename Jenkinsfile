pipeline {
    agent any
   
    tools
    {
    maven "mvn-3.9.9"    
    }
	
    triggers {
        githubPush()
    }
    stages {
        stage('git checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Modiashok247/javacode.git'
            }
        }
        stage('build') {
            steps {
                sh "mvn clean package"
            }
        }
        stage('sonar report') {
            steps {
                sh "mvn sonar:sonar"
            }
        }
        stage('nexus artifactory') {
            steps {
                sh "mvn clean deploy"
            }
        }
        stage('tomcat deploy')
    {
        steps{
         sh """
            curl -u ashok:password \
            --upload-file /var/lib/jenkins/workspace/Jio-declarative-pl/target/maven-web-application.war \
            "http://16.16.184.255:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """   
        }
    }
    }//stages end
	
}//pipline end
