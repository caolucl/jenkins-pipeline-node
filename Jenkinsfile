pipeline {
    environment {
        registry = "acrlcaotest1.azurecr.io/node/pipeline"
        registryCredential = 'azure-docker-registry'
        link_registry = "https://acrlcaotest1.azurecr.io/node/pipeline"
    }
    /*
    agent {
        dockerfile {
            filename 'Dockerfile'
        }
    }
    */
    
    stages {
        stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

            git clone 'https://github.com/caolucl/jenkins-pipeline-node'
        }
        stage('Build image') {
            app = docker.build("node/pipeline")
        
        
        stage('Running node') {
            steps {
                    app.inside {
                    sh 'npm start & '
                }
                
            }
        }
        
        stage('Check connection') {
            steps {
                app.inside {
                    sh 'curl http://127.0.0.1:8000 || exit 1'
                }
            }
        }
        stage('Push image') {
            /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
             docker.withRegistry( 'https://acrlcaotest1.azurecr.io/node/pipeline', registryCredential ) {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
             }    
         }
    }
}
