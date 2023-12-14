pipeline {
    agent any

   tools {
       go 'go-1.21.3'
    }

    stages {
        stage('Unit Test') {
            steps {
                script {
                    sh 'go mod init hello'
                    sh 'go test'
                }
            }
        }

        stage('Coverage Report') {
            steps {
                script {
                    sh 'go test -coverprofile=coverage.out'
                    sh 'go tool cover -html=coverage.out -o coverage.html'
                }
                archiveArtifacts 'coverage.html'
            }
        }

        stage('Build') {
            steps {
                script {
                    // Adjust these commands based on how you build and upload your Go application to Nexus
                    sh 'go build -o main .'
                    // sh 'curl -u username:password -X PUT --upload-file your-app https://nexus.example.com/repository/your-repo/your-app/1.0.0/your-app-1.0.0'
                }
                archiveArtifacts 'main'
            }
        }

        stage('Build Docker Image') {
           steps {
               script {
                    // build docker image
                   //sh 'docker build -t dab8106/hellogo .'
               }
           }
       }

        stage('Push Docker Image') {
           steps {
               script {
                    //Push docker image in specific server
                   }
               }
           }
       }
    }

    post {
        always {
            cleanWs()
        }
    }
}