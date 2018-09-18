pipeline {
    agent any
    environment { 
    def COV_DIR = "/home/ylei/cov-analysis-linux64/bin"
    }
    stages{
        stage('Build'){
            steps {
                sh 'echo $COV_DIR'
                sh './configure'
                sh 'make'
            }
            post {
                success {
                    echo 'Build successfully!'
                }
            }
        }
        stage('Clean'){
            steps {
                sh 'make clean'
            }
            post {
                success {
                    echo 'Analyzed by Coverity successfully!'
                }
            }
        }
        stage('Coverity build'){
            steps {
                sh '$COV_DIR/cov-build --dir idir make'
            }
        }
        stage('Coverity analyze'){
            steps {
                sh '$COV_DIR/cov-analyze --dir idir --all'
            }
        }
        stage('Coverity commit'){
            steps {
                sh '$COV_DIR/cov-commit-defects --dir idir --host ylei-5520 --user admin --auth-key-file auth-key-admin --stream proftpd'
            }
        }
    }
}