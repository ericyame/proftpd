pipeline {
    agent any
    environment { 
    def COV_DIR = "/home/ylei/cov-analysis-linux64/bin"
    }
    stages{
        stage('Black Duck Hub Detect scan'){
            steps {
              sh 'echo BD'
              sh 'bash <(curl -s https://blackducksoftware.github.io/hub-detect/hub-detect.sh) --blackduck.url=https://ylei-virtualbox --blackduck.api.token=NjAyYjY5ZWQtZTU5NC00ZTUzLTgxMDYtNWM4ODIwYjQ5MmNmOjYyZmNkYTQzLWRmZjItNDk3Ni04ZWZiLTI3Y2U5Yzc5YjQ2Yw== --blackduck.trust.cert=true --detect.project.name=proftpd_pipeline --detect.project.version.name=1.0 --detect.tools.excluded=POLARIS --detect.source.path=.'
            }
            post {
                success {
                    echo 'Black Duck Hub Detect scan successfully!'
                }
                failure {
                    echo 'Black Duck Hub Detect scan failed!'
                }
            }
        }
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
        }
        stage('Coverity build'){
            steps {
                sh '$COV_DIR/cov-build --dir idir make'
            }
            post {
                success {
                    echo 'Coverity build successfully!'
                }
                failure {
                    echo 'Coverity build failed!'
                }
            }
        }
        stage('Coverity analyze'){
            steps {
                sh '$COV_DIR/cov-analyze --dir idir --all'
            }
            post {
                success {
                    echo 'Coverity analyze successfully!'
                }
                failure {
                    echo 'Coverity analyze failed!'
                }
            }
        }
        stage('Coverity commit'){
            steps {
                sh '$COV_DIR/cov-commit-defects --dir idir --host ylei-5520 --port 8089 --auth-key-file $COV_DIR/auth-key-admin --stream proftpd'
            }
            post {
                success {
                    echo 'Coverity commit successfully!'
                }
                failure {
                    echo 'Coverity commit failed!'
                }
            }
        }
    }
}
