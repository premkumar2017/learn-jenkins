### Jenkins Declarative Pipeline -> Git Verify Stage Setup

Setup/Update the Jenkins Declarative Pipeline to meet the below requirements:

Update your Jenkins Pipeline Devops.

Add a new stage named as 'Git-Verify'

Setup the command under steps section 'git --version'

Build the Pipeline to print the Docker Version and Git Version in the output

Answer

Just add new stage as git-verify in the existing pipeline configuration and check build the pipeline
Pipeline configuration

```

pipeline {
    agent any

    stages {
        stage('Docker-Verify') {
            steps {
                echo 'docker --version'
            }
        }
        stage('git-verify'){
            steps {
                sh 'git --version'
            }
        }
        
    }
}

```

![image](https://github.com/user-attachments/assets/4f89d1a3-3682-4c5e-8e6d-aeaaeef6e50e)

![image](https://github.com/user-attachments/assets/41dbf9e5-533b-4d5a-be32-c17fe1b60588)

