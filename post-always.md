### **Steps to Update the Jenkinsfile:**
1. **Go to GitLab Repo** and open the `Jenkinsfile`.
2. **Modify the Jenkinsfile** to add a `post` section at the pipeline level.
3. **Add an `always` block** inside the `post` section.
4. **Include the command:**  
   ```sh
   sudo docker images
   ```
   This will list all Docker images every time the pipeline runs, regardless of success or failure.
5. **Save and commit** the updated Jenkinsfile.
6. **Run the DevOps pipeline** in Jenkins to validate the changes.

---

### **Updated Jenkinsfile with `post` Section**
```groovy
pipeline {
    agent any

    options {
        timestamps()
        skipDefaultCheckout()
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '10'))
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
                        sleep 30
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
                expression { return env.GIT_BRANCH == "origin/main" }
            }
            steps {
                sh "docker build -t ${Docker_Image_Name}:${env.BUILD_NUMBER} ."
                sh "docker inspect ${Docker_Image_Name}:${env.BUILD_NUMBER}"
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
                sh "sudo docker run -itd -p 80:80 ${Docker_Image_Name}:${env.BUILD_NUMBER}"
                sh "sudo docker ps"
            }
        }
        stage('Docker-Images-CleanUp') {
            steps {
                sh 'sudo docker image prune -af'
            }
        }
    }

    post {
        always {
            sh 'sudo docker images'
        }
    }
}
```

---

### **Explanation of Updates:**
✅ **Added `post` section** at the pipeline level.  
✅ **Used `always` block** to ensure the step runs after every pipeline execution.  
✅ **Included `sh 'sudo docker images'`** to display all Docker images.  
✅ **Maintained best practices** like `disableConcurrentBuilds()` and `buildDiscarder(logRotator(numToKeepStr: '10'))`.

---

### **Next Steps:**
✔ **Commit and push** the updated `Jenkinsfile` to GitLab.  
✔ **Trigger the DevOps pipeline** in Jenkins to validate the changes.  

Let me know if you need further modifications! 🚀


![image](https://github.com/user-attachments/assets/95867006-9e29-4145-9ce2-56d8c50b5d38)
