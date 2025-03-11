

🎯 Why These Changes?
skipDefaultCheckout(): Prevents automatic git checkout in Jenkins (useful if you manually check out the code elsewhere in the pipeline).
docker inspect: Helps verify that the image is correctly built and contains the expected metadata



![image](https://github.com/user-attachments/assets/ea84a3a8-7b9e-46c1-b284-5f3f8d7a87ce)

🚀 Next Steps:
Update Dockerfile in GitLab (change LABEL name="devops" to LABEL name="AutoPilot")
Update Jenkinsfile and commit the changes
Run the DevOps pipeline in Jenkins
Verify logs to ensure the pipeline runs correctly



![image](https://github.com/user-attachments/assets/b399a41e-d962-442b-b308-b0a4e461c729)

New label has not been updated

![image](https://github.com/user-attachments/assets/65ab6078-69d3-4e4e-92c0-1356d3affb72)


