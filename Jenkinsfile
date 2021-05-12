pipeline {
    agent any


    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                git branch: 'Grupa03-KM306474_Lab07', url: 'https://github.com/InzynieriaOprogramowaniaAGH/MIFT2021'
                dir('Grupy/Grupa03/KM306474/Lab07/Docker'){
                    
                    sh '''
                        curl -L "https://github.com/docker/compose/releases/download/1.29.1/docker-compose-$(uname -s)-$(uname -m)" -o ~/docker-compose
                        chmod +x ~/docker-compose
                        ~/docker-compose up -d docker-build
                        ls -l
                        docker --version
                    ''' 
                }

            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            
                git branch: 'Grupa03-KM306474_Lab07', url: 'https://github.com/InzynieriaOprogramowaniaAGH/MIFT2021'
                dir('Grupy/Grupa03/KM306474/Lab07/Docker'){
                    
                    sh '''
                        ~/docker-compose up -d docker-test
                    ''' 

                }
            }
        }
    }
    post{
        success {
            emailext attachLog: true,
                to: 'kiksdeiksde@gmail.com',
                subject: "Success ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}"
        }
        failure {
            emailext attachLog: true,
                to: 'kiksdeiksde@gmail.com',
                subject: "Failed  ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}"
        }
    }
}