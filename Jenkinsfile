pipeline {
    agent { label 'ec2-node' }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rinas-ck/build-deploy-using-maven.git'
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
