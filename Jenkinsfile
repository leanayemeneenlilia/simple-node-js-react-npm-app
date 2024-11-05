pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            // Définir l'argument `args` pour inclure le chemin absolu dans un format compatible Windows.
            args '-p 3000:3000 -v /c/ProgramData/Jenkins/.jenkins/workspace/simple-node-js-react-npm-app:/workspace -w /workspace'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
