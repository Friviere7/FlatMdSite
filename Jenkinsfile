pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', changelog: false, credentialsId: 'git-ssh', url: 'git@github.com:Friviere7/FlatMdSite.git'
            }
        }
        
        stage('Build') {
            parallel {
                stage('Liste fichiers') {
                    steps {
                        sh 'ls -ail > fichiers.txt'
                    }
                }
                stage('Liste processus') {
                    steps {
                        sh 'ps aux > processus.txt'
                    }
                }
            }
        }
                stage('Validation HTML') {
                    steps {
                        script {
                           
                            sh 'tidy -q -e _template_.html'
                        }
                    }
                }    
    }
    post {
        success {
            archiveArtifacts artifacts: 'fichiers.txt, processus.txt', followSymlinks: false
        }
    }
}

