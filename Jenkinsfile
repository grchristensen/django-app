pipeline {
    agent none
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:3'
                }
            }
            steps {
                withEnv(["HOME=${env.WORKSPACE}"]) {
                  sh "pip install -r requirements.txt --user"
                }
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'python:3'
                }
            }
            steps {
                withEnv(["HOME=${env.WORKSPACE}"]) {
                    sh "pip install -r requirements.txt --user"
                    sh 'python manage.py test'
                }
            }
        }
        stage('Deliver') {
            agent any
//             environment {
//                 VOLUME = '$(pwd)/sources:/src'
//                 IMAGE = 'cdrx/pyinstaller-linux:python2'
//             }
            steps {
                sh 'docker build -t django-app .'
            }
//             post {
//                 success {
//                     archiveArtifacts "${env.BUILD_ID}/sources/dist/add2vals"
//                     sh "docker run --rm -v ${VOLUME} ${IMAGE} 'rm -rf build dist'"
//                 }
//             }
        }
    }
}