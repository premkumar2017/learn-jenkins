###  Add Docker Build Stage

Go to GitLab Repo

Update your JenkinsFile to add one more stage named as 'Docker-Build'

Inside the Steps section of stage 'Docker-Build' add a command 'sudo docker build -t my-container .'

Then Run the DevOps Pipeline after Jenkinsfile is updated

![image](https://github.com/user-attachments/assets/784c9d95-128c-41da-909e-071ba85a7241)


In case you are facing issue while running the pipeline, check the jenkins logs

![image](https://github.com/user-attachments/assets/02be7d70-d281-4ac1-a956-9fef7c8ee542)

provide sudo access to jenkins

![image](https://github.com/user-attachments/assets/a0e48a34-8fd3-488a-ab33-ff0a67277b09)

make sure jenkins is part of docker group

![image](https://github.com/user-attachments/assets/1bf7feea-611f-44cf-b320-0c36c3fd3fb9)

Now build is successfull

![image](https://github.com/user-attachments/assets/df666b30-da21-4d62-a3c2-425e05e91391)


---
**+ sudo docker build -t my-container:v1 .

sudo: a terminal is required to read the password; either use the -S option to read from standard input or configure an askpass helper

sudo: a password is required

script returned exit code 1

It looks like Jenkins is running as a user that is **not in the `sudoers` group**, causing permission issues when executing Docker commands. Here’s how you can fix this:******

---

### ✅ **Solution 1: Add Jenkins to the Docker Group (Recommended)**
Instead of using `sudo`, allow the `jenkins` user to run Docker directly.

1. **Check if the `docker` group exists**  
   ```sh
   cat /etc/group | grep docker
   ```
   If no output, create the group:
   ```sh
   sudo groupadd docker
   ```

2. **Add Jenkins to the `docker` group**  
   ```sh
   sudo usermod -aG docker jenkins
   ```

3. **Restart Jenkins & Docker**  
   ```sh
   sudo systemctl restart docker
   sudo systemctl restart jenkins
   ```

4. **Test if Jenkins can run Docker without sudo**  
   Run this inside a Jenkins job:
   ```sh
   docker ps
   ```

---

### ✅ **Solution 2: Allow Jenkins to Use `sudo` Without a Password**  
If Solution 1 doesn’t work, allow Jenkins to use `sudo` for Docker commands.

1. Open the `sudoers` file:
   ```sh
   sudo visudo
   ```

2. Add this line at the end:
   ```
   jenkins ALL=(ALL) NOPASSWD: /usr/bin/docker
   ```

3. Save & Exit (`CTRL+X`, then `Y`, then `ENTER`).

4. Modify the Jenkins pipeline or job to use `sudo`:
   ```sh
   sudo docker build -t my-container:v1 .
   ```

---

### ✅ **Solution 3: Run Jenkins in Docker With Docker Socket (Alternative)**
If Jenkins is running in a **Docker container**, you can mount the host Docker socket to give it access:
```sh
docker run -d --name jenkins \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins/jenkins:lts
```
This allows Jenkins inside the container to communicate with the host’s Docker.

---

### 🎯 **Best Approach?**
- ✅ **For security & best practices:** Use **Solution 1** (Add Jenkins to `docker` group).
- 🔴 **If needed for automation:** Use **Solution 2** (`sudo` without a password).
- 🐳 **If running Jenkins in Docker:** Use **Solution 3** (Docker socket).

Try these and let me know which works for you! 🚀
