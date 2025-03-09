### Have to check the error

### Task 3 - Jenkins Free Style Job -> Parameters

Setup the Jenkins Free Style Job to meet the below requirements:

Update your Free Style Jenkins Job Docker-Verify

Remove the cron from the job to avoid running it every minute.

Configure your job as parameterized job , add choice section in your job.

Under the choices section add two options , docker and python.

Then update your execute shell command to get the version of package selected by the user.

Click on configure and select the parameterize option
![image](https://github.com/user-attachments/assets/ef41cba1-e3e4-4513-96ae-82394c4edd5f)

Select choice parameter

![image](https://github.com/user-attachments/assets/3bb3aef5-9194-404d-a7e1-49de5ea935d3)

once package is given, scroll down and change the hard coded value from docker --version to $package --version


![image](https://github.com/user-attachments/assets/7ea653bd-43ae-4fce-9b95-40fcda0a28c4)

After that select Build with parameters

![image](https://github.com/user-attachments/assets/acdac34a-0933-4a6a-8c36-0abda4588b10)






