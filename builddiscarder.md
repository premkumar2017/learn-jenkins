The `buildDiscarder` option in Jenkins helps manage build history efficiently. Here are its key benefits:

1. **Saves Disk Space**: It prevents Jenkins from storing excessive build logs, artifacts, and metadata, reducing storage usage.
2. **Improves Performance**: Keeping fewer builds helps Jenkins run faster by reducing the load on the system.
3. **Enhances Log Management**: Keeps the workspace clean by retaining only relevant build logs.
4. **Reduces Clutter**: Helps teams focus on the most recent builds without unnecessary old logs.
5. **Automates Cleanup**: Eliminates the need for manual deletion of old builds.

By setting `logRotator(numToKeepStr: '1')`, you ensure that only the latest build logs are kept, optimizing Jenkins performance and storage. 🚀

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


The Jenkinsfile has been updated with the following changes:
- `numToKeepStr` value changed to **10** to retain logs of the last 10 builds.
- Added **`sleep 30`** in the `Docker-Verify` stage. 
- Included **`disableConcurrentBuilds()`** to prevent parallel executions.

Now, proceed to GitLab and trigger the **DevOps Pipeline** to apply the changes. 🚀

The disableConcurrentBuilds() option in Jenkins prevents multiple builds of the same pipeline from running simultaneously. Here are its key benefits:

Avoids Resource Conflicts: Prevents issues with shared resources (e.g., files, databases, or Docker containers) being accessed by multiple builds at the same time.
Ensures Build Consistency: Ensures only one build runs at a time, preventing unpredictable behavior caused by overlapping executions.
Reduces Load on Jenkins: Helps optimize system performance by limiting concurrent executions, which is especially useful for resource-intensive pipelines.


![image](https://github.com/user-attachments/assets/556ca007-f80f-472e-bf1f-cae675ec6eba)
