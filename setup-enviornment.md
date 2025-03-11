### Setup Environment Variables

Go to GitLab Repo

Update your JenkinsFile to add 2 environment variables :

Docker_Image_Name = 'my-container'

Docker_Tag = 'v2'

Inside the Steps section of stage 'Docker-Build' update the docker build command to use the variables for docker image name and tag name

Then Run the DevOps Pipeline after Jenkinsfile is updated


![image](https://github.com/user-attachments/assets/71708cf0-3d5c-4b15-8c85-44fc7e341101)

![Uploading image.png…]()


