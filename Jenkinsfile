pipeline {
    agent any 
    stages {
        stage('Cleanup') {
            steps {
                sh 'rm -rf QRPA'
            }
        }
        
        stage('Checkout') {
            steps {
                sh 'git clone https://github.com/Aldee01/QRPA.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'docker build -t aldee01/qrpa QRPA '
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
                sh 'aws ecs update-service --cluster aldee_claster --service alain_service --force-new-deployment --region ca-central-1'
            }
        }
       
        }
    }
