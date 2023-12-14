pipeline {
    agent any

   tools {
       go 'go-1.21.3'
    }

    environment {
        //SONAR_TOKEN = credentials('SONAR_TOKEN') // Reference Jenkins credential ID
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

        // stage('Run SonarQube Analysis') {
        //     steps {
        //         script {
        //                 sh '/usr/local/sonar/bin/sonar-scanner -X -Dsonar.organization=wm-demo -Dsonar.projectKey=wm-demo_hello-webapp-golang -Dsonar.sources=. -Dsonar.host.url=https://sonarcloud.io'
        //         }
        //     }
        // }

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
                   //sh 'docker build -t dab8106/hellogo .'
               }
           }
       }

        stage('Push Docker Image') {
           steps {
               script {
                //    withCredentials([usernamePassword(credentialsId: 'DOCKER_REGISTRY_CREDENTIALS_ID', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                //        sh """
                //            echo $DOCKER_PASSWORD | docker login --username $DOCKER_USERNAME --password-stdin
                //            docker push dab8106/hellogo
                //        """
                //    }
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