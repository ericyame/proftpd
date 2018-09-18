pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                bat './configure'
                bat 'make'
            }
            post {
                success {
                    echo 'Build successfully!'
                }
            }
        }
    }
}