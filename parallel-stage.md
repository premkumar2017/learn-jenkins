
🎯 What is the Use of Parallel Stages?


Parallel execution helps speed up the pipeline by running independent tasks at the same time.

✅ Benefits:

Faster execution: Instead of running Docker-Verify and Git-Verify one after the other, they now run simultaneously.
Efficient resource usage: Utilizes Jenkins agents better.
Reduces pipeline runtime, especially useful for large builds.
In your case:

Docker-Verify and Git-Verify don’t depend on each other.
Running them in parallel inside Pre-Checks makes the pipeline faster.

![image](https://github.com/user-attachments/assets/82ca8b66-dab6-4e37-be3a-8ad4d457ed9b)


![image](https://github.com/user-attachments/assets/0562bccb-9450-4c11-9c7c-004cc8d21b51)
