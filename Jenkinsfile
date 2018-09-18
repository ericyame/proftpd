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
    }
}