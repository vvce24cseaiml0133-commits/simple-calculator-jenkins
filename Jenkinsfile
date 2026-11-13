
pipeline {
    agent any

    stages {
        stage('SCM Synchronization') {
            steps {
                echo 'Pulling latest code changes from Git repository...'
                checkout scm
            }
        }

        stage('Static Verification') {
            steps {
                echo 'Checking Maven project layout rules...'
                bat '"C:\\apache-maven-3.10.0\\bin\\mvn.cmd" validate'
            }
        }

        stage('Compilation & Automated Testing') {
            steps {
                echo 'Compiling and running automated tests...'
                bat '"C:\\apache-maven-3.10.0\\bin\\mvn.cmd" clean package'
            }
            post {
                always {
                    echo 'Publishing unit test reports...'
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully! Code stability confirmed.'
        }
        failure {
            echo 'CI Pipeline failed and broken. Check console logs.'
        }
    }
}
