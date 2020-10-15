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
                script {
                    // Checkout the repository and save the resulting metadata
                    def scmVars = checkout([
                        $class: 'GitSCM'
                    ])

                    // Display the variable using scmVars
                    echo "scmVars.GIT_COMMIT"
                    echo "${scmVars.GIT_COMMIT}"

                    // Displaying the variables saving it as environment variable
                    env.GIT_COMMIT = scmVars.GIT_COMMIT
                    echo "env.GIT_COMMIT"
                    echo "${env.GIT_COMMIT}"
                }                 
                git branch: 'main',
                    credentialsId: 'github-andrea',
                    url: 'https://github.com/andrea-colleoni/kaldevops-projects.git'
                bat 'dir'
            }
        }
    }
}
