
---

# Flask RealWorld Example App

**Software Re-Engineering – Assignment 1**
**Containerization & Static Code Analysis**

---

## 📌 Assignment Details

**Assignment No:** 1
**Topic:** Containerization & Static Code Analysis

### 👥 Group Members

| Name           | Roll Number |
| -------------- | ----------- |
| M. Hashim Ali  | 22F3635     |
| Sarmad Mehmood | 22F3695     |

---

## 📖 Project Overview

This repository contains a **containerized version of the Flask RealWorld Example App**.
The project has been enhanced with:

* **Docker** for containerization
* **SonarQube** for static code analysis

### 🔗 Original Repository

* [https://github.com/gothinkster/flask-realworld-example-app](https://github.com/gothinkster/flask-realworld-example-app)

### 🛠 Tech Stack

* **Language:** Python
* **Framework:** Flask
* **Tools:** Docker, SonarQube

---

## 🐳 Docker Execution Steps

Follow the steps below to build and run the application using Docker.

### ✅ Prerequisites

* Docker Desktop installed and running

---

### Step 1: Clone the Repository

```bash
git clone https://github.com/gothinkster/flask-realworld-example-app
cd flask-realworld-example-app
```

---

### Step 2: Build the Docker Image

This command builds the Docker image using the `Dockerfile` in the root directory.

```bash
docker build -t flask-realworld .
```

---

### Step 3: Run the Container

Run the container and expose port **5000**.

```bash
docker run -p 5000:5000 flask-realworld
```

---

### 🔍 Verification

Open your browser and navigate to:

```
http://localhost:5000/api/articles
```

If the API response is displayed, the container is running successfully.

---

## 🔎 SonarQube Analysis Steps

Follow the steps below to deploy SonarQube and analyze the project.

---

### Step 1: Deploy SonarQube Server

Pull and run the official SonarQube Community Edition image.

```bash
docker pull sonarqube:community
docker run -d --name sonarqube -p 9000:9000 sonarqube:community
```

📊 **Access Dashboard:**

```
http://localhost:9000
```

🔐 **Default Login:**

* Username: `admin`
* Password: `admin`
  (You will be prompted to change the password)

---

### Step 2: Configure Project & Token

1. Log in to SonarQube
2. Click **Create a local project**
3. Set the following:

   * **Project Key:** `flask-realworld`
   * **Main Branch:** `master`
4. Choose **Use the global setting**
5. Select **Locally** as the analysis method
6. Generate a token named `my-token` and copy it

---

### Step 3: Run SonarScanner

Run the scanner from the **root directory** of the project.

🔁 Replace `[YOUR_TOKEN_HERE]` with your generated token.

#### 🪟 Windows (PowerShell)

```powershell
docker run --rm `
  -e SONAR_HOST_URL="http://host.docker.internal:9000" `
  -e SONAR_SCANNER_OPTS="-Dsonar.projectKey=flask-realworld" `
  -e SONAR_TOKEN="[YOUR_TOKEN_HERE]" `
  -v "${PWD}:/usr/src" `
  sonarsource/sonar-scanner-cli
```

#### 🐧 Linux / 🍎 macOS / Git Bash

```bash
docker run --rm \
  -e SONAR_HOST_URL="http://host.docker.internal:9000" \
  -e SONAR_SCANNER_OPTS="-Dsonar.projectKey=flask-realworld" \
  -e SONAR_TOKEN="[YOUR_TOKEN_HERE]" \
  -v "${PWD}:/usr/src" \
  sonarsource/sonar-scanner-cli
```

---

### Step 4: View Results

After the scan completes (look for **`EXECUTION SUCCESS`** in the terminal):

* Refresh the SonarQube dashboard at

  ```
  http://localhost:9000
  ```
* View code quality metrics, bugs, vulnerabilities, and code smells

---