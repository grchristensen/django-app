pipeline {
    agent { dockerfile true }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Test') {
            steps {
                sh 'python manage.py test'
            }
        }
    }
}
