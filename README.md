# Multi-Container Docker Application with CI/CD: Calculator App Project

### Submission by - **Yuhan Fu**

## Project Overview

### **Brief project description:**

The Calculator App is a web-based application that provides basic arithmetic functionality, including addition, subtraction, multiplication, and division. The app consists of a frontend built with React and a backend API implemented in Python using Flask. The services are containerized with Docker, and a CI/CD pipeline is set up for automated building and deployment.

### Implemented Components

- `Dockerfiles`: Used to build Docker images for the frontend and backend services.
- `docker-compose.yml`: Defines the multi-container setup, including frontend (React) and backend (Flask) services, ensuring they can communicate and run independently in Docker containers.
- `.gitlab-ci.yml`: Defines the stages (build, test, docker, deploy) for automating the build, test, Docker image creation, and deployment process.

### Docker Implementation

- **Backend Dockerfile** (Python API):
  The backend Dockerfile uses a Python image to containerize the Flask app. It installs dependencies and exposes the required port for communication with the frontend.

- **Frontend Dockerfile** (React App):
  The frontend Dockerfile builds the React app and serves it via Nginx. It installs the required Node.js dependencies, builds the app, and copies the assets into the Nginx image to serve them.

### Docker Compose YAML Configuration

- **Services:** React frontend app that builds and serves the frontend via Nginx. Python Flask backend API that handles the calculation requests.
- **Networking:** The services are connected via Docker's internal network, allowing the frontend to communicate with the backend API using an internal API URL.
- **Ports:** The frontend is exposed on port 3000, and the backend is exposed on port 5000 to handle API requests.
- **Environment Variables:** Configuration such as port numbers and the API URL for the frontend to access the backend are defined as environment variables.

### CI/CD Pipeline (YAML Configuration)

- **Stages**:
  - **Build**: The pipeline first builds the frontend and backend services, ensuring that all dependencies are installed and the applications are ready to run.
  - **Test**: The backend code is tested using pytest to ensure that all calculations and API functions work correctly.
  - **Docker**: After successful builds and tests, Docker images for both the frontend and backend are built and pushed to Docker Hub.
  - **Deploy**: Finally, the images are deployed, or the system is prepared for production.
- **Jobs**:
  - `frontend-job`: builds the frontend application by installing dependencies and running the build script using Node.js.
  - `backend-build-job` and `backend-test-job`: handle the installation of backend dependencies and run tests using pytest to verify the API functionality.
  - `docker-build`: builds Docker images for both the frontend and backend services and pushes them to the Docker registry if on the main branch.
  - `deploy`: handle the process of deploying the Docker images to a production environment.

### Assumptions

- The backend and frontend applications are assumed to be pre-configured and working locally.

### Lessons Learned

- The use of multi-stage Dockerfiles helped reduce the size of the images, while Docker Compose made it easy to manage the interaction between the frontend and backend.
- Automating the deployment process with a CI/CD pipeline significantly reduced manual intervention and made the development process more efficient.

### Future Improvements

- The Dockerfiles could be optimized further to use smaller base images or make use of Docker caching to speed up the build process.
- The pipeline could be expanded to include more advanced testing stages, such as linting or end-to-end testing, and support multiple deployment environments.
