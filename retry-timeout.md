## Jenkins pipeline with retry and timeout only for Docker-Verify

🛠 Key Features & Behavior:
Timeout (timeout(time: x, unit: 'MINUTES'))

Stops a stage if it exceeds the given time (prevents infinite hangs).
Example: Docker-Build has a 5-minute limit to prevent long-running builds.
Retry (retry(n) {})

If a command fails, it retries up to n times before marking the stage as failed.
Example: Git-Verify retries 2 times if git --version fails.


![image](https://github.com/user-attachments/assets/e6603c9c-8f7f-4731-b2d9-fa6c849a263b)


 How This Works:
⏳ Timeout: The Docker-Verify stage fails if it takes more than 1 minute.
🔄 Retry: If docker --version fails, Jenkins retries up to 3 times before marking the stage as failed.



