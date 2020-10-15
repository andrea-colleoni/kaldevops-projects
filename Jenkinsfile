pipeline {
    agent any

    stages {
        stage('Project info') {
            steps {
                echo "Project: ${currentBuild.projectName}"
                echo "Build #: ${currentBuild.number}"
            }
        }        
        stage("Clean WS") {
            steps {
                cleanWs()
            }
        }
        stage("git checkout") {
            steps {
                git branch: 'main',
                    credentialsId: 'github-andrea',
                    url: 'https://github.com/andrea-colleoni/kaldevops-projects.git'
                bat 'dir'
            }
        }
    }
}
