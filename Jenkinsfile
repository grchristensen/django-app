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
            environment {
//                 registry = "YourDockerhubAccount/YourRepository"
                registryCredential = 'dockerhub_id'
//                 dockerImage = ''
            }
            steps {
                sh 'docker build -t grchr/tdd-django-app:1.0 .'
            }
            post {
                success {
                    script {
                        docker.withRegistry( '', registryCredential ) {
                            sh 'docker push grchr/tdd-django-app:1.0'
                        }
                    }
                }
            }
        }
    }
}