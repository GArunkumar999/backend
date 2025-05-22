pipeline{
    agent { label 'AGENT-1' }
    environment{
        project="expense"
        component="backend"
        DEPLOY_TO="production"
    }
    options { 
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        }
    stages{
        stage('ReadVersion'){
            steps{
                script{
                    def packageJson = readJSON file: 'package.version'
                    appVersion = packageJson.version
                    echo "Version is: $appVersion"
                }
            }
        }

        stage('deploy'){
            //     input {
            //     message "Should we continue?"
            //     ok "Yes, we should."
            //     submitter "alice,bob"
            //     parameters {
            //         string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
            //     }
            // }
            when { 
                environment name: 'DEPLOY_TO', value: 'production'
            }
            steps{
                script{
                    echo "This is deploy"
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