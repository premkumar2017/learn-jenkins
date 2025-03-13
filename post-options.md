### **Scenario Introduction: Handling Success & Failure in Jenkins Pipeline**  

In a **Jenkins Pipeline**, different execution scenarios can occur, and we need to handle them properly. The three most common scenarios are **success**, **failure**, and **aborted**. Jenkins provides a **post** section to define actions based on these outcomes.

---

### **Scenario 1: Successful Execution (`success`)**  
✅ **What Happens?**  
- All pipeline stages execute successfully without errors.  
- The pipeline reaches the final stage and completes.  
- Logs will indicate the pipeline finished successfully.  

✅ **How to Handle?**  
- Notify users about successful deployment.  
- Send an email or Slack notification.  
- Log the success message.  

✅ **Example Code:**  
```groovy
post {
    success {
        echo 'Pipeline executed successfully!'
    }
}
```

---

### **Scenario 2: Failure (`failure`)**  
❌ **What Happens?**  
- A stage fails due to an error in the script, such as a Docker build failure or a missing dependency.  
- The pipeline stops at the failed stage.  
- Jenkins logs the failure and marks the build as **failed**.  

❌ **How to Handle?**  
- Notify users about the failure.  
- Capture logs for debugging.  
- Trigger a rollback or cleanup process.  

❌ **Example Code:**  
```groovy
post {
    failure {
        echo 'Pipeline failed! Investigate the issue.'
        sh 'sudo docker ps'  // Check running containers in case of a failure
    }
}
```

---

### **Scenario 3: Aborted Execution (`aborted`)**  
🛑 **What Happens?**  
- The pipeline is **manually stopped** by the user or by Jenkins due to external factors.  
- It may happen due to **manual intervention** or a **timeout setting**.  
- Jenkins logs indicate the build was aborted.  

🛑 **How to Handle?**  
- Log an appropriate message.  
- Notify stakeholders.  
- Perform cleanup actions if needed.  

🛑 **Example Code:**  
```groovy
post {
    aborted {
        echo 'Pipeline was aborted!'
        sh 'sudo docker ps'  // Check if any containers are still running
    }
}
```

---

### **Final Enhanced `post` Section**
Here’s how we integrate all three scenarios into our Jenkinsfile:
```groovy
post {
    always {
        sh 'sudo docker images'
    }
    success {
        echo 'Pipeline executed successfully! Deployment was completed.'
    }
    failure {
        echo 'Pipeline failed! Investigate the issue.'
        sh 'sudo docker ps'
    }
    aborted {
        echo 'Pipeline was aborted by the user!'
        sh 'sudo docker ps'
    }
}
```

---

### **Example Execution Scenarios**
| Scenario  | Example Cause | Jenkins Outcome | Post-Action |
|-----------|-------------|----------------|-------------|
| ✅ **Success** | Docker image builds and deploys correctly | Marked as `SUCCESS` | Logs success message |
| ❌ **Failure** | Docker build fails due to missing dependencies | Marked as `FAILURE` | Logs error, checks running containers |
| 🛑 **Aborted** | User manually stops the pipeline | Marked as `ABORTED` | Logs the action, checks running containers |

---

### **Conclusion**
By handling success, failure, and aborted scenarios properly, we ensure:
✅ Clear logs for debugging  
✅ Automated notifications for stakeholders  
✅ System cleanup to avoid resource wastage  

Would you like to integrate **email notifications** for failures? 🚀

![image](https://github.com/user-attachments/assets/261597de-579a-4b67-aa46-4bbe03219575)


Execution Flow
1️⃣ Verifies Docker and Git installation.
2️⃣ Builds Docker Image only if on the main branch.
3️⃣ Shows available Docker images.
4️⃣ Asks for manual approval before deploying the container.
5️⃣ Cleans up unused images after deployment.
6️⃣ Handles all post scenarios (success, failure, and abort).
