pipeline {
    /*
    agent {
        dockerfile {
            filename 'Dockerfile'
        }
    }
    */
    agent none
    stages {
        stage('Cloning Git') {
          steps {
            git 'https://https://github.com/caolucl/jenkins-pipeline-node'
          }
        }
        stage('execute') { 
            steps {
                script {
                    img = docker.build("node/pipeline")
                    
                    img.inside('--entrypoint= -e NODE_ENV=test') {
                        sh 'npm install --dev'
                        sh 'npm run test'
                    }                   
                }
            }
        }
        stage('Check file') {
            steps {
                /*
                sh 'npm start &'
                sh 'wait $!'
                */
                img.inside(){
                     sh 'curl http://127.0.0.1:8000 || exit 1'
                }
               
            }
        }
    }
}
