pipeline {
    agent any 
    stages {
        
        stage('Build') {
            steps {
                sh 'docker build -t aldee01/qrpa .'
            }
        }
        
        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Aldeedockerpass', usernameVariable: 'Alpha', passwordVariable: 'AlphaPass')]) {
                    sh '''
                      docker login -u "$Alpha" -p "$AlphaPass"
                      docker push aldee01/qrpa
                    '''
                }
            }
        }
        
        stage('Deploy') {
            steps {
               sh 'echo developement done'
               // sh 'aws ecs update-service --cluster aldee_claster --service alain_service --force-new-deployment --region ca-central-1'
            }
        }
       
        }
    }
