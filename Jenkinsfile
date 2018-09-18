pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
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
                sh 'PATH=/home/ylei/cov-analysis-linux64/bin:$PATH'
                sh 'export PATH'
                sh 'echo $PATH'
                sh 'cov-build --dir idir make'
            }
        }
        stage('Coverity analyze'){
            steps {
                sh 'cov-analyze --dir idir --all'
            }
        }
        stage('Coverity commit'){
            steps {
                sh 'cov-commit-defects --dir idir --host ylei-5520 --user admin --auth-key-file auth-key-admin --stream proftpd'
            }
        }
    }
}