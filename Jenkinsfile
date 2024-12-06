pipeline {
  agent any
  
   tools {nodejs "node"}
    
  stages {
    stage("Clone code from GitHub") {
            steps {
                script {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GITHUB_CREDENTIALS', url: 'https://github.com/123Vasu/v_12']])
                }
            }
        }
     
    stage('Node JS Build') {
      steps {
        bat 'npm install'
      }
    }
  
     stage('Build Node JS Docker Image') {
            steps {
                script {
                  bat 'docker build -t va1234567/nodeapp:latest .'
                }
            }
        }


        stage('Deploy Docker Image to DockerHub') {
            steps {
                script {
                withCredentials([string(credentialsId: 'Vasu12345', variable: 'Vasu12345')]) {
                    bat 'docker login -u va1234567 -p %Vasu12345%'
            }
            bat 'docker push va1234567/nodeapp:latest'
        }
            }   
        }
         
     stage('Deploying Node App to Kubernetes') {
       steps {
        script {    
          kubernetesDeploy(configs: "nodeapp.yaml", kubeconfigId: "kubernetes")
        }
      }
      }
    }
  }