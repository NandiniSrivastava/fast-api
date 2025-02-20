# 🚀 FastAPI Dockerized Application
This project is a FastAPI-based web service that provides user details when accessed. The application is containerized using Docker and includes a GitHub Actions workflow for automated deployment.

## 📌 Features
✅ FastAPI framework for building APIs
✅ Dockerized for easy deployment
✅ GitHub Actions for CI/CD
✅ GET endpoint to retrieve user details

## 🛠️ Installation and Running Locally
🔹 1. Clone the Repository
sh
Copy
git clone <your-repo-url>
cd <your-project-folder>
🔹 2. Create a Virtual Environment (Optional)
sh
Copy
python -m venv venv
source venv/bin/activate  # On macOS/Linux
venv\Scripts\activate     # On Windows
🔹 3. Install Dependencies
sh
Copy
pip install fastapi uvicorn
🔹 4. Run the FastAPI Server Locally
sh
Copy
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
Open http://127.0.0.1:8000/ in a browser.

## 🚢 Building and Running the Docker Image
🔹 1. Build the Docker Image
sh
Copy
docker build -t nandinisrivastava/my-image:v0.1 .
🔹 2. Run the Container
sh
Copy
docker run -d -p 8000:8000 nandinisrivastava/my-image:v0.1
Open http://localhost:8000/ in a browser.
🔹 3. Check Running Containers
sh
Copy
docker ps
🔹 4. View Container Logs
sh
Copy
docker logs <container_id>

## 📌 API Endpoints
Method	Endpoint	Description
GET	/	Returns user details
GET	/{data}	Returns { "hi": data }
Example:

sh
Copy
curl http://127.0.0.1:8000/Nandini
Response:

json
Copy
{
  "hi": "Nandini"
}

## ⚡ GitHub Actions Workflow Explanation
This repository includes a GitHub Actions workflow for automatic Docker image builds and pushes to Docker Hub.

🔹 Workflow File: .github/workflows/docker-build.yml
yaml
Copy
name: Build and Push Docker Image

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Log in to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build Docker Image
        run: docker build -t nandinisrivastava/my-image:v0.1 .

      - name: Push Docker Image
        run: docker push nandinisrivastava/my-image:v0.1
🔹 What This Workflow Does:
Triggers on push and pull requests to the main branch.
Checks out the repository.
Logs into Docker Hub using stored credentials.
Builds the Docker image with the specified tag.
Pushes the image to Docker Hub.

## 🔑 Setting Up Docker Token and Secrets in GitHub
To allow GitHub Actions to push Docker images to your Docker Hub repository, follow these steps:

Step 1: Generate a Docker Hub Access Token
1️⃣ Log in to Docker Hub.
2️⃣ Go to Account Settings → Security.
3️⃣ Click "New Access Token", give it a name, and select read/write access.
4️⃣ Copy the generated token.

Step 2: Add Secrets to GitHub Repository
1️⃣ Go to your GitHub repository.
2️⃣ Click on "Settings" → "Secrets and variables" → "Actions".
3️⃣ Click "New repository secret" and add:

DOCKER_USERNAME → Your Docker Hub username
DOCKER_PASSWORD → Paste the Docker token copied earlier
4️⃣ Save the secrets.

Step 3: Trigger the Workflow
Push a commit to the main branch to automatically build and push the image to Docker Hub.

## 🔥 Troubleshooting
1️⃣ "Cannot access 0.0.0.0:8000"
➡️ Use http://127.0.0.1:8000/ or http://localhost:8000/ instead.

2️⃣ "Container Exited"

sh
Copy
docker ps -a
docker logs <container_id>
➡️ Fix errors in dependencies (pip install fastapi uvicorn).

3️⃣ "uvicorn: command not found"
➡️ Ensure FastAPI and Uvicorn are installed inside the container.

### Screenshot
![image](https://github.com/user-attachments/assets/31c92451-8013-4dde-b267-6a2ac92fba78)


![image](https://github.com/user-attachments/assets/3d817e10-4004-4b9c-908d-6910e10886f6)


![image](https://github.com/user-attachments/assets/4a29c7ae-ebae-47c1-8600-fb71c351c8d7)

