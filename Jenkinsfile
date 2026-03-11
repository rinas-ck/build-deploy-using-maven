pipeline {
    agent { label 'ec2' }

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
        sh '''
        sudo mkdir -p /opt/app
        sudo cp target/*.jar /opt/app/

        cd /opt/app
        JAR=$(ls *.jar | head -n 1)
        nohup java -jar $JAR > app.log 2>&1 &
    #hii    '''
    }
    
}
    }
}
