pipeline{
    agent { label 'AGENT-1' }
    environment{
        project="expense"
        component="backend"
        appVersion=''
        ACC_ID = 435238037339
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
                   withAWS(region: 'us-east-1', credentials: 'aws-cred'){
                    sh """
                   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com
                   docker build -t ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${project}/${component}:${appVersion}
                   docker push ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${project}/${component}:${appVersion}
                   """
                   }
                   
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
       
    }
}