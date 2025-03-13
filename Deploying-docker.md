```
pipeline {
    agent any

    options {
        timestamps()  // Enables timestamps in logs
        skipDefaultCheckout()  // Prevents Jenkins from automatically checking out the repository
        buildDiscarder(logRotator(numToKeepStr: '10'))  // Keeps logs of last 10 builds
        disableConcurrentBuilds()  // Prevents concurrent builds
    }

    environment {
        Docker_Image_Name = 'my-container'
        Docker_Tag = 'v2'
    }

    stages {
        stage('Pre-Checks') {
            parallel {
                stage('Docker-Verify') {
                    steps {
                        retry(3) {
                            sh 'docker --version'
                        }
                        sh 'sleep 30'  // Adding sleep for 30 seconds
                    }
                }
                stage('Git-Verify') {
                    steps {
                        sh 'git --version'
                    }
                }
            }
        }
        stage('Docker-Build') {
            when {
                expression {
                    return env.GIT_BRANCH == "origin/main"
                }
            }
            steps {
                sh "docker build -t ${Docker_Image_Name}:${env.BUILD_NUMBER} ."
                sh "docker inspect ${Docker_Image_Name}:${env.BUILD_NUMBER}"  // Inspect the built image
            }
        }
        stage('Docker-Image') {
            steps {
                sh 'docker images'
            }
        }
        stage('Docker-Deploy') {
            steps {
                sh "sudo docker run -itd -p 80:80 ${Docker_Image_Name}:${env.BUILD_NUMBER}"  // Deploy the container
                sh "sudo docker ps"  // Check running containers
            }
        }
    }
}

```

![image](https://github.com/user-attachments/assets/cb39fac7-f74c-4300-847f-57a24d0894f2)
