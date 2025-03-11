### JenkinsFile SCM GitLab Integration


If you have created the Jenkinsfile on GitLab , it time to update the Devops Pipeline

So go to Jenkins and update the Pipeline Definition section , change the Pipeline Script option to Pipeline Script from SCM

Then select SCM as Git

Add the Repo Clone HTTPS URL in Repository URL section

For Credentials , Create Username and Password type of credentials with your GitLab email/password

Update the Branch to Main and click save


![image](https://github.com/user-attachments/assets/1f540e91-f9b4-4c4d-a1eb-3dadc682d9b4)

It is time to build jenkin piple via scm using git integration. Run build now and see the whether pipeline is running or not

![image](https://github.com/user-attachments/assets/45b49d76-a16e-454d-872d-01d917726ca4)






