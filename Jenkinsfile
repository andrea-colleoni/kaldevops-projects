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
                    def scmVars = checkout(
                        [
                            $class: 'GitSCM', branches: [[name: '*/main']], 
                            doGenerateSubmoduleConfigurations: false, 
                            extensions: [], 
                            submoduleCfg: [], 
                            userRemoteConfigs: 
                            [
                                [
                                    credentialsId: 'github-andrea', 
                                    url: 'https://github.com/andrea-colleoni/kaldevops-projects'
                                ]
                            ]
                        ]
                    )
                    env.GIT_COMMIT = scmVars.GIT_COMMIT
                } 
                bat 'dir'
            }
        }
        stage("write build info") {
            steps {
                writeFile file: 'buikd-info.md', text: """# Informazioni build

                    - Progetto: ${currentBuild.projectName}-${currentBuild.number}
                    - Data build: ${ new Date().format(\'yyyy-MM-dd HH:mm:ss\')}
                    - SHA1 git commit: ${env.GIT_COMMIT}"""
            }
        }
        stage('maven compile') {
            steps {
                withMaven(jdk: 'JDK 14', maven: 'Maven 3.6.3') {
                    bat 'mvn -f ./sts/devops-project/pom.xml test'
                }
            }
        }
    }
}
