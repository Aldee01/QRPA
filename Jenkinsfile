pipeline {
    agent any 
    stages {
        
        stage('Build') {
            steps {
                sh 'docker build -t aldee01/qrpa .'
            }
        }

         stage('Sonarqube analysis') {
             environment {
              scanner-home = tool 'sonnar-scanner'
            steps {
                withSonarQubeEnv(credentialsId: 'SONAR_TOKEN', installationName: 'Dave')
                {
                    sh '''
                        sonar-scanner \
                          -Dsonar.organization=aldee01 \
                          -Dsonar.projectKey=aldee01_newproject \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=https://sonarcloud.io
                      ''' 
                }
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
