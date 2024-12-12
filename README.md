# Containerization of the Application: React Frontend, Node.js Backend, and MongoDB Database

## To containerize a multi-component web application involving a React frontend, a Node.js backend, and a MongoDB database using Docker and Docker Compose. The containerization allows for consistent development environments, easy deployment, and scalability.

Frontend repository: : https://github.com/Anand-1432/Techdome-frontend

Backend repository: : https://github.com/Anand-1432/Techdome-backend

## Approach

### 1. Dockerizing the Frontend
The React frontend is containerized using a Dockerfile. It sets up a Node.js base image, copies the source code, installs production dependencies, and exposes the application on port 3000.

```
FROM node
WORKDIR /usr/src/app
COPY . .
RUN npm install --production
EXPOSE 3000
CMD ["npm", "start"]

```
This ensures that the React application can run inside a Docker container without requiring additional setups on the host machine.

### 2. Dockerizing the Backend
The Node.js backend is containerized using the provided Dockerfile (Dockerfile-backend). The file includes instructions to set up the environment, install dependencies, and expose the backend application on port 5000.
```
FROM node
WORKDIR /usr/src/app
COPY . .
RUN npm install
EXPOSE 5000
CMD ["npm", "start"]

```
### 3.Utilized mongodb image for database
MongoDB, the database for this application, is containerized using its official image. It stores data persistently using a Docker volume (mongo-data) and exposes port 27017 for database connections.
```
docker run -d --name mongo -p 27017:27017 --network react mongo:latest
```
### 4. Orchestrating with Docker Compose
A docker-compose.yaml file is used to define and manage the services (frontend, backend, and MongoDB) as part of a single application.

#### Key Components of docker-compose.yaml:

**Networks**: A shared network reactapp enables communication between the containers.
**Volumes**: A named volume mongo-data ensures database data persists across container restarts.
**Environment Variables**: Configuration settings (e.g., REACT_APP_BASE_URL and database connection strings) are injected into the services for dynamic setups.

### Tools Used
Docker: Used to create container images for the frontend, backend, and database.
Docker Compose: Simplifies the orchestration of multiple containers, managing services and interconnections.
Node.js: Provides a runtime environment for JavaScript applications in the frontend and backend.
MongoDB: A NoSQL database used for persistent data storage.
Docker Hub: For pulling the official MongoDB image.

## Steps to Deploy
1. Build Docker Images:
```
docker build -t frontend -f Dockerfile-frontend .
docker build -t backend -f Dockerfile-backend .

```
2. Execute the compose file:

3. Access the application on browser with instance IP and port 3000
