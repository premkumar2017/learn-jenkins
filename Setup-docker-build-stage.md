###  Add Docker Build Stage

Go to GitLab Repo

Update your JenkinsFile to add one more stage named as 'Docker-Build'

Inside the Steps section of stage 'Docker-Build' add a command 'sudo docker build -t my-container .'

Then Run the DevOps Pipeline after Jenkinsfile is updated

![image](https://github.com/user-attachments/assets/784c9d95-128c-41da-909e-071ba85a7241)


In case you are facing issue in the build jenkins the following, check the jenkins logs

![image](https://github.com/user-attachments/assets/02be7d70-d281-4ac1-a956-9fef7c8ee542)

provide sudo access to jenkins

![image](https://github.com/user-attachments/assets/a0e48a34-8fd3-488a-ab33-ff0a67277b09)

make sure jenkins is part of docker group

![image](https://github.com/user-attachments/assets/1bf7feea-611f-44cf-b320-0c36c3fd3fb9)

Now build is successfull

![image](https://github.com/user-attachments/assets/df666b30-da21-4d62-a3c2-425e05e91391)



