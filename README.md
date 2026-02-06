Flask RealWorld Example App - Software Re-Engineering Assignment 1

Assignment: No. 1 - Containerization & Static Code Analysis

Group Members

Name

Roll Number

M. Hashim Ali

22F3635

Sarmad Mehmood

22F3695

Project Overview

This repository contains a containerized version of the Flask RealWorld Example App. The project has been updated with a Dockerfile for containerization and analyzed using SonarQube for static code analysis.

Original Repository: https://github.com/gothinkster/flask-realworld-example-app

Language: Python (Flask)

1. Docker Execution Steps

Follow these steps to build and run the application container.

Prerequisites

Docker Desktop installed and running.

Step 1: Clone the Repository

git clone <YOUR_FORK_URL>
cd flask-realworld-example-app


Step 2: Build the Docker Image

This command builds the image using the Dockerfile in the root directory.

docker build -t flask-realworld .


Step 3: Run the Container

Run the container and map port 5000.

docker run -p 5000:5000 flask-realworld


Verification:
Open your browser and navigate to: http://localhost:5000/api/articles to see the API response.

2. SonarQube Analysis Steps

Follow these steps to deploy SonarQube and run the static analysis scanner.

Step 1: Deploy SonarQube Server

Pull and run the official SonarQube Community Edition image.

docker pull sonarqube:community
docker run -d --name sonarqube -p 9000:9000 sonarqube:community


Access Dashboard: Open http://localhost:9000

Default Login: admin / admin (You will be prompted to change the password).

Step 2: Configure Project & Token

Log in to SonarQube.

Click "Create a local project".

Project Key: flask-realworld.

Main Branch: master.

Select "Use the global setting" for defining the project.

Select "Locally" for analysis method.

Generate a token named my-token and copy it.

Step 3: Run SonarScanner

Execute the scanner using Docker. Run this command from the root of the project folder.

Replace [YOUR_TOKEN_HERE] with the token generated in the previous step.

Windows (PowerShell):

docker run --rm `
    -e SONAR_HOST_URL="[http://host.docker.internal:9000](http://host.docker.internal:9000)" `
    -e SONAR_SCANNER_OPTS="-Dsonar.projectKey=flask-realworld" `
    -e SONAR_TOKEN="[YOUR_TOKEN_HERE]" `
    -v "${PWD}:/usr/src" `
    sonarsource/sonar-scanner-cli


Linux / Mac / Git Bash:

docker run --rm \
    -e SONAR_HOST_URL="[http://host.docker.internal:9000](http://host.docker.internal:9000)" \
    -e SONAR_SCANNER_OPTS="-Dsonar.projectKey=flask-realworld" \
    -e SONAR_TOKEN="[YOUR_TOKEN_HERE]" \
    -v "${PWD}:/usr/src" \
    sonarsource/sonar-scanner-cli


Step 4: View Results

Once the scan is complete (look for EXECUTION SUCCESS in the terminal), refresh your SonarQube dashboard at http://localhost:9000 to view the analysis report.