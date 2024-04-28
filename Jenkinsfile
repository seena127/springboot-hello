pipeline {
    agent any 
    tools {
        maven "3.8.4"
    
    }
    stages {
        stage('Compile and Clean') { 
            steps {
                // Run Maven on a Unix agent.
              
                sh "mvn clean compile"
            }
        }
        stage('deploy') { 
            
            steps {
                sh "mvn package"
            }
        }
        stage('Build Docker image'){
          
            steps {
                echo "Hello Java Express"
                sh 'ls'
                sh 'docker build -t  bsreenu1999/docker_jenkins_springboot .'
            }
        }
        stage('Docker Login'){
            
            steps {
                 withCredentials([string(credentialsId: 'DockerId', variable: 'Dockerpwd')]) {
                    sh "docker login -u bsreenu1999 -p ${Dockerpwd}"
                }
            }                
        }
        stage('Docker Push'){
            steps {
                sh 'docker push bsreenu1999/docker_jenkins_springboot'
            }
        }
        stage('Docker deploy'){
            steps {
               
                sh 'docker run -itd -p  8081:8080 bsreenu1999/docker_jenkins_springboot'
            }
        }
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}

