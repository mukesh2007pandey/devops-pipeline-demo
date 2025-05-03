## DevOps Demo Pipeline
This project demonstrates:
- Git versioning
- Jenkins CI/CD pipeline
- Docker containerization
- Ansible deployment

### Prerequisites
- Jenkins with Docker and Ansible plugins
- Ansible installed
- DockerHub account

### Run Manually
```bash
docker build -t devops-demo .
docker run -p 80:5000 devops-demo
```

### CI/CD Flow
1. Push to GitHub
2. Jenkins builds Docker image
3. Pushes to DockerHub
4. Ansible deploys to remote server

