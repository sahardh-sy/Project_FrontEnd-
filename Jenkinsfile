pipeline {
    agent any
   
    stages {
      
      
        stage("Build image"){
            steps {

                sh '''
                
                docker build -t sahar24/front:${IMAGETAG}  . 

                '''

                  echo 'image builded'
            }
        }
        stage("Push image"){
            steps {
                 script{
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub-cred',
                    usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                        env.REG_USERNAME = USERNAME
                        env.REG_PASSWORD = PASSWORD
                    }

               sh ''' 
               docker login --username=${REG_USERNAME} --password=${REG_PASSWORD}
                docker push sahar24/front:${IMAGETAG} 
                '''

            }
            }
        }

       

    }

     environment {
        
       
        IMAGETAG = "${env.BUILD_ID}"
    }
}
