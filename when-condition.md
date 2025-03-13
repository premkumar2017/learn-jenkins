The **`when`** condition in Jenkins pipelines is used to control the execution of a stage based on specific conditions.  

### **Key Benefits of `when` Condition:**
1. **Conditional Execution**: Ensures that a stage runs only when certain conditions are met (e.g., specific branch, changes in files, or environment variables).  
2. **Optimized Builds**: Prevents unnecessary execution of stages, reducing build time and resource usage.  
3. **Branch-Specific Logic**: Allows different workflows for different branches, such as deploying only from the `main` branch.  
4. **Better Control Over CI/CD**: Ensures that critical processes (like deployment) only happen under the right conditions.  

### **Example Use Cases:**
- **Run a stage only on `main` branch:**
  ```groovy
  when {
      expression { return env.GIT_BRANCH == "origin/main" }
  }
  ```
- **Run a stage if a file has changed:**
  ```groovy
  when {
      changeset "src/**"
  }
  ```
- **Run a stage based on environment variables:**
  ```groovy
  when {
      environment name: 'DEPLOY_ENV', value: 'production'
  }
  ```

This makes pipelines **dynamic, efficient, and flexible** in a CI/CD workflow. 🚀

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
                    return env.GIT_BRANCH == "origin/test"
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
    }
}

```

![image](https://github.com/user-attachments/assets/13b1947e-6b5a-4438-aead-1a0f45225ae3)
