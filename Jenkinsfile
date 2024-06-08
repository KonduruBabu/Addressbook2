pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
                git url:'https://github.com/KonduruBabu/Addressbook2.git/', branch: "master"
            }
        }
        stage('Build') {
            steps {
               sh "mvn clean package"
            }
        }
       
        stage('Build Image') {
            steps {
                sh 'docker build -t babukonduru/imgaddbook:latest .'
                sh 'docker image'
            }
        }
        stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockercred', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push babukonduru/imgaddbook:latest'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    def dockerCmd = 'docker run -itd --name My-first-containe211 -p 80:8082 babukonduru/imgaddbook:latest'
                    sshagent(['sshkeypair']) {
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.25 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
