pipeline {
    agent {
        dockerfile {
            filename 'Dockerfile'
        }
    }
    stages {
        stage('Check file') {
            steps {
                /*
                sh 'npm start &'
                sh 'wait $!'
                */
                sh 'curl http://127.0.0.1 || exit 1'
            }
        }
    }
}
