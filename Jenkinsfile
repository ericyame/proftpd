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
        stage('Coverity'){
            steps {
                sh 'make clean'
                sh 'cov-build --dir idir make'
                sh 'cov-analyze --dir idir --all'
                sh 'cov-commit-defects --dir idir --host ylei-5520 --user admin --auth-key-file auth-key-admin --stream proftpd'
            }
            post {
                success {
                    echo 'Analyzed by Coverity successfully!'
                }
            }
        }
    }
}