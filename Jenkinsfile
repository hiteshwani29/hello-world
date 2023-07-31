pipeline{
    agent {
        kubernetes {
            label 'maven-agent'
        }
    }   
    tools {
        maven 'Installer'
    }
    stages {
        stage("clone repository"){
            steps{
                git 'https://github.com/hiteshwani29/hello-world'
            }
        }
        stage("maven build"){
            steps{
               sh 'mvn clean install'
            }
        }
    }
    
    
    post {
        success {
            // Deploy the WAR to Tomcat using the "Deploy to container" plugin
            step([
                $class: 'DeployPublisher',
                adapters: [
                    [$class: 'Tomcat8xAdapter', credentialsId: 'tomcat-deployer', url: 'http://18.205.185.91:8080/'],
                ],
                war: '**/*.war'
            ])
        }
    }
}
