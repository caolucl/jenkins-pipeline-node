pipeline {
    agent {
        dockerfile {
            filename 'Dockerfile'
        }
    }
    stages {
        stage('Check file') {
            steps {
                sh 'npm start & && wait $!'
                sh 'curl http://127.0.0.1 || exit 1'
            }
        }
    }
}
