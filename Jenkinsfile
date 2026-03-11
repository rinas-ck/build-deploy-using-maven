pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/rinas-ck/build-deploy-using-maven.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh 'cp target/*.jar /opt/app/'
            }
        }
    }
}
