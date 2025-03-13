
### Explanation of `input` Step in Jenkinsfile  

The **`input` step** in Jenkins declarative pipelines is used to **pause the pipeline execution** and ask for **manual approval** before proceeding to the next steps.

#### **Syntax in the 'Docker-Deploy' Stage**  
```groovy
input {
    message "Do you want to proceed for deployment ?"
}
```

#### **How It Works**  
1. **Pipeline Execution Stops:** When the pipeline reaches the **Docker-Deploy** stage, it **pauses execution**.  
2. **User Approval Required:** Jenkins displays a prompt with the message:  
   - **"Do you want to proceed for deployment?"**  
   - The user must **manually approve** the step in the Jenkins UI.  
3. **Pipeline Resumes or Aborts:**  
   - If the user **approves**, the pipeline proceeds with deployment.  
   - If the user **rejects or ignores** it, the pipeline will stay paused until action is taken or it times out.

#### **Use Cases**  
- Ensures that deployment happens only after **human verification**.  
- Useful for **production deployments** where manual intervention is necessary.  
- Prevents accidental deployments due to automated triggers.

Would you like to customize this further (e.g., add a timeout or specific user roles for approval)? 😊



```
pipeline {
    agent any

    options {
        timestamps()  // Enables timestamps in logs
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
                script {
                  input message: "Do you want to proceed for deployment?"
                }
                sh "sudo docker run -itd -p 80:80 ${Docker_Image_Name}:${env.BUILD_NUMBER}"  // Deploy the container
                sh "sudo docker ps"  // Check running containers
            }
        }
    }
}
```

![image](https://github.com/user-attachments/assets/10fd6f4a-e220-4318-9034-576cc67bb259)
