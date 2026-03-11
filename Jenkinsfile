pipeline {
    agent any

    tools {
        maven 'maven-3.9'
        jdk 'jdk17'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/rinas-ck/build-deploy-using-maven.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh '''
                        echo "Copying artifact to EC2..."
                        scp -o StrictHostKeyChecking=no \
                            target/demo-1.0.0.jar \
                            ubuntu@13.61.19.22:/opt/app/

                        echo "Starting application on EC2..."
                        ssh -T -o StrictHostKeyChecking=no ubuntu@<EC2_PUBLIC_IP> '
                            pkill -f demo-1.0.0.jar || true
                            setsid nohup java -jar /opt/app/demo-1.0.0.jar \
                                > /opt/app/app.log 2>&1 < /dev/null &
                            exit 0
                        '
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "Deployment completed successfully."
        }
        failure {
            echo "Deployment failed. Check Jenkins or EC2 logs."
        }
    }
}
