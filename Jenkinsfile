pipeline{
    agent { label 'AGENT-1' }
    environment{
        project="expense"
        component="backend"
        appVersion=''
    }
    options { 
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        }
    stages{
        stage('ReadVersion'){
            steps{
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "Version is: $appVersion"
                }
            }
        }

        stage('Install Dependencies'){
            steps{
                script{
                  sh """
                     npm install

                     """    
                }
            }
        }
        stage('Build image'){
            steps{
                script{
                   sh 'docker build -t backend:1.0.0 .'
                }
            }
        }
        
    }
    post{
        always{
            echo "say hello always"
            deleteDir()
        }
        success{
            echo "say hello in success"
        }
        failure{
            echo "say hello in failure"
        }
        unsuccessful{
            echo "say hello in unsuccessful"
        }
    }
}