# Day 25 Answer : Complete Jenkins CI/CD Project - Continued with Documentation

You've been making amazing progress, so let's take a moment to catch up and refine our work. Today's focus is on completing the Jenkins CI/CD project from Day 24 and creating thorough documentation for it.

## Did you finish Day 24?

- Day 24 provided an end-to-end project experience, and adding this to your resume will be a significant achievement.

- Take your time to finish the project, create comprehensive documentation, and make sure to highlight it in your resume and share your experience.

## Task 1 : Answer

# CI/CD Deployment using Jenkins, GitHub Webhooks and Docker Compose

## 📌 Project Overview

This project demonstrates how to automate application deployment using **GitHub, Jenkins, Docker, and Docker Compose**.
The pipeline is triggered automatically whenever code is pushed to the repository. Jenkins receives the webhook event from GitHub and deploys the updated application using Docker Compose.

This README documents the **complete setup process from cloning the repository to deployment**.

---

# 🧰 Tools & Technologies Used

* Git
* GitHub
* Jenkins
* Docker
* Docker Compose
* Linux (Ubuntu Server / EC2)

---

# 📁 Project Workflow

Developer pushes code → GitHub repository → Webhook triggers Jenkins → Jenkins pulls latest code → Docker Compose builds & runs containers → Application deployed.

---

# 1️⃣ Clone the Repository

First clone the repository to your system or Jenkins server.

```bash
git clone https://github.com/<your-username>/<repository-name>.git
```

Navigate into the project directory.

```bash
cd <repository-name>
```

---

# 2️⃣ Install Required Dependencies

Make sure the Jenkins server has the following tools installed.

## Install Git

```bash
sudo apt update
sudo apt install git -y
```

## Install Docker

```bash
sudo apt install docker.io -y
```

Start Docker service.

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

Allow Jenkins to run Docker commands.

```bash
sudo usermod -aG docker jenkins
```

Restart Jenkins.

```bash
sudo systemctl restart jenkins
```

---

## Install Docker Compose

```bash
sudo apt install docker-compose -y
```

Verify installation.

```bash
docker --version
docker-compose --version
```

---

# 3️⃣ Create Docker Compose Configuration

Create a file named:

```
docker-compose.yml
```

Example configuration:

```yaml
version: "3"

services:
  app:
    build: .
    container_name: node_app
    ports:
      - "3000:3000"
    restart: always
```

### Explanation

| Section  | Purpose                          |
| -------- | -------------------------------- |
| version  | Compose file version             |
| services | Defines containers               |
| build    | Builds image from Dockerfile     |
| ports    | Maps container port to host      |
| restart  | Restarts container automatically |

---

# 4️⃣ Push Changes to GitHub

After creating the Docker Compose file, push the changes.

```bash
git add .
git commit -m "Added docker compose configuration"
git push origin main
```

---

# 5️⃣ Configure Jenkins Job

Open Jenkins in your browser.

```
http://<server-ip>:8080
```

### Create a Job

1. Click **New Item**
2. Enter job name
3. Select **Freestyle Project**
4. Click **OK**

---

# 6️⃣ Connect Jenkins to GitHub Repository

Inside Jenkins job configuration:

### Source Code Management

Select **Git**

Enter repository URL:

```
https://github.com/<username>/<repository>.git
```

Branch:

```
*/main
```

---

# 7️⃣ Configure Build Trigger

Scroll to **Build Triggers** and enable:

```
GitHub hook trigger for GITScm polling
```

This allows Jenkins to trigger builds automatically when GitHub sends webhook events.

---

# 8️⃣ Add Build Steps (Execute Shell)

In **Build → Execute Shell**, add the following commands:

```bash
echo "Stopping previous containers"
docker-compose down || true

echo "Building and starting containers"
docker-compose up -d --build

echo "Checking running containers"
docker ps
```

### What These Commands Do

docker-compose down → Stops existing containers
docker-compose up -d --build → Builds and runs containers
docker ps → Shows running containers

---

# 9️⃣ Configure GitHub Webhook

Go to your GitHub repository.

Navigate to:

```
Settings → Webhooks → Add Webhook
```

### Fill the Following Details

**Payload URL**

```
http://<jenkins-server-ip>:8080/github-webhook/
```

**Content Type**

```
application/json
```

**Events**

```
Just the push event
```

Click **Add Webhook**.

---

# 🔟 Test the CI/CD Pipeline

Push a change to the repository.

```bash
git add .
git commit -m "Testing webhook trigger"
git push
```

GitHub will send a webhook event to Jenkins.

---

# 1️⃣1️⃣ Jenkins Build Execution

Once Jenkins receives the webhook:

1. Jenkins pulls the latest code
2. Executes the shell commands
3. Builds Docker images
4. Runs containers using Docker Compose

You can view logs in:

```
Jenkins → Job → Build History → Console Output
```

---

# 1️⃣2️⃣ Verify Running Containers

Check running containers on the server.

```bash
docker ps
```

Example output:

```
CONTAINER ID   IMAGE      PORTS
123abc         node_app   0.0.0.0:3000->3000
```

---

# 1️⃣3️⃣ Access the Application

Open the browser:

```
http://<server-ip>:3000
```

Your application should now be running.

---

# 🎉 CI/CD Pipeline Completed

The automated pipeline now works as follows:

```
Code Push
   ↓
GitHub Repository
   ↓
Webhook Trigger
   ↓
Jenkins Pipeline
   ↓
Docker Compose Build
   ↓
Container Deployment
   ↓
Application Running
```

---

# 📌 Future Improvements

Possible enhancements to this project:

* Convert Jenkins job to Pipeline (Jenkinsfile)
* Push Docker images to Docker registry
* Add automated testing stage
* Deploy to Kubernetes
* Add monitoring and logging

---

# 📚 Conclusion

This project demonstrates a simple but powerful CI/CD workflow that automates deployment using Jenkins, GitHub Webhooks, and Docker Compose.
Documenting the process helps in understanding the pipeline and makes it easier for others to replicate or contribute to the project.

---

⭐ If you found this project useful, consider giving it a star!





