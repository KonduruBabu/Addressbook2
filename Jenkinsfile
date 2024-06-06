pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/KonduruBabu/Addressbook2'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                // Install Tomcat9 on the Jenkins server or a separate server
                // Deploy the packaged application (WAR file) to Tomcat9
                // Verify the application deployment using a browser
            }
        }
    }
}
