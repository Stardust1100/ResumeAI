# Resume Q&A Chatbot

## Overview

Resume Q&A Chatbot is designed to assist hiring managers and recruiters by answering questions related to your resume, skills, experience, projects, and other relevant information. The chatbot is built using Vue.js for the frontend, Flask for the backend, and AWS SageMaker for NLP and machine learning.

## Features

- Interactive chat interface for users
- Natural Language Processing (NLP) using AWS SageMaker
- Flask backend to handle chatbot logic
- PostgreSQL database for storing resume details and FAQs
- CI/CD pipeline with GitHub Actions and Docker
- Deployed on AWS for scalability and availability

## Technologies

- Frontend: Vue.js
- Backend: Flask (Python)
- NLP and Machine Learning: AWS SageMaker
- Database: PostgreSQL
- CI/CD: GitHub Actions, Docker
- Cloud Services: AWS (EC2/Fargate, S3, CloudWatch)

## Getting Started

### Prerequisites

- Node.js and npm
- Python 3.x and virtualenv
- PostgreSQL
- AWS account with SageMaker and EC2 access

### Installation

1. **Clone the repository:**

    ```bash
    git clone https://github.com/your-username/resume-chatbot.git
    cd resume-chatbot
    ```

2. **Set up the frontend:**

    ```bash
    cd frontend
    npm install
    npm run serve
    ```

3. **Set up the backend:**

    ```bash
    cd ../backend
    python -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
    ```

4. **Configure PostgreSQL:**

    - Create a new PostgreSQL database and user.
    - Update the database connection details in `backend/app.py`.

    ```python
    conn = psycopg2.connect(
        dbname="resume_chatbot",
        user="chatbot_user",
        password="yourpassword",
        host="localhost"
    )
    ```

5. **Run the Flask backend:**

    ```bash
    flask run
    ```

### Deploying to AWS

1. **Build and push Docker image:**

    ```bash
    docker build -t mychatbot .
    docker tag mychatbot:latest myrepo/mychatbot:latest
    echo ${{ secrets.DOCKER_PASSWORD }} | docker login -u ${{ secrets.DOCKER_USERNAME }} --password-stdin
    docker push myrepo/mychatbot:latest
    ```

2. **Deploy on AWS (EC2 or Fargate):**

    Follow AWS documentation to deploy the Docker container on EC2 or Fargate.

### Setting Up CI/CD

1. **Configure GitHub Actions:**

    Create a `.github/workflows/main.yml` file with the following content:

    ```yaml
    name: CI/CD Pipeline

    on: [push]

    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v2
        - name: Set up Python
          uses: actions/setup-python@v2
          with:
            python-version: '3.8'
        - name: Install dependencies
          run: |
            python -m pip install --upgrade pip
            pip install -r backend/requirements.txt
        - name: Run tests
          run: |
            cd backend
            python -m unittest discover
        - name: Build and push Docker image
          run: |
            docker build -t mychatbot .
            docker tag mychatbot:latest myrepo/mychatbot:latest
            echo ${{ secrets.DOCKER_PASSWORD }} | docker login -u ${{ secrets.DOCKER_USERNAME }} --password-stdin
            docker push myrepo/mychatbot:latest
    ```

### Contributing

Feel free to open issues or submit pull requests with improvements and bug fixes. All contributions are welcome!

### License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
