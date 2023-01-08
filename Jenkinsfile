pipeline {
    agent any
    environment{
    registry="sahar24/front_back"
    registryCredential='dockerHub'
    dokerImage="front_back"
    }
    
    stages {
  
        stage('Git Preparation') {
            steps {
                cleanWs()
                checkout scm
                sh 'git rev-parse --short HEAD > .git/commit-id'
                script {
                    commit_id = readFile('.git/commit-id').trim()  
                }
            }
        }
        

        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build --prod'
            }


        }
        stage('Build Docker image ') {
           
            steps {
                script {
                    dockerImage = docker.build imageName + ":${commit_id}"
                }
            }
        stage("docker push") {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()   
                }
                }
            }
        }
        stage('Cleaning up') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}