# Jenkins Pipeline Project using Git, Docker, and Email Notifications

## 📘 Project Overview
This project demonstrates how to use **Jenkins plugins** like **Git**, **Docker**, and **Email Notifications** to automate a Continuous Integration (CI) pipeline.

The pipeline automatically:
1. Pulls source code from a GitHub repository  
2. Builds a Docker image  
3. Runs the container  
4. Sends an email notification when the build succeeds or fails  

---

## 🛠️ Tools & Technologies Used
- **Jenkins**
- **Git & GitHub**
- **Docker**
- **Email Extension Plugin (Jenkins)**
- **Python** (sample app, can use any language)

---

## ⚙️ How the Pipeline Works
1. **Checkout Stage:** Jenkins pulls the latest code from GitHub  
2. **Build Stage:** Builds a Docker image using the Dockerfile  
3. **Run Stage:** Runs the application inside a Docker container  
4. **Post Actions:** Sends success/failure email notifications  

---

## 🧩 Folder Structure
