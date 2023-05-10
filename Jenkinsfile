pipeline {
    agent any

    //environment {
    //    DOCKERHUB_CREDENTIALS = credentials('stir-docker-chris')
    //}

    stages {
        stage('Build') {
            steps {
                container('maven') {
                    sh """
                    mvn install -DskipTests=true -Dmaven.javadoc.skip=true -B -V 
                    """
                }
            }
        }
        stage('Test') {
            steps {
                container('maven') {
                    sh """
                    mvn test -B 
                    """
                }
            }
        }
        /*
        stage('Docker Build') {
            steps {
                container('docker') {
                    sh """
                    docker build -t docker.stir.ac.uk:5000/backupview:$BUILD_NUMBER -f ./build/Dockerfile .
                    """
                }
            }
        }
        stage('Docker Login') {
            steps {
                container('docker') {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin docker.stir.ac.uk:5000'
                }
            }
        }

        stage('Docker Push') {
            steps {
                container('docker') {
                    sh 'docker push docker.stir.ac.uk:5000/backupview:$BUILD_NUMBER'
                }
            }
        }
        */
    }
    post {
        always {
            container('docker') {
                sh 'docker logout'
            }
        }
    }
}
