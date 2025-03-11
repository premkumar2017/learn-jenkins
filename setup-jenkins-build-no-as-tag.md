### Jenkins Pre Defined Variables

Go to GitLab Repo

Inside the Steps section of stage 'Docker-Build' update the docker build command to use the Jenkins Build Number as tag value, So basically the tag value of our docker image will be always updated.

Use :  ${env.BUILD_NUMBER}


![image](https://github.com/user-attachments/assets/11001bd4-6a90-4a6b-9b34-bfadb337507f)


Then Run the DevOps Pipeline after Jenkinsfile is updated

![image](https://github.com/user-attachments/assets/c6c1ff22-b8ab-4caf-8e9d-a2b1b3d4afa5)
