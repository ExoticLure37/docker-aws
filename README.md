# Docker AWS

A learning-focused project inspired by Sheriyan Coding School's Docker-AWS repository, created for experimentation and understanding how Docker and AWS deployment patterns work together.

This project combines a React frontend and an Express + Socket.IO backend to serve a real-time collaborative coding experience. The app is built so that the frontend is compiled into the backend's `public` directory and then served from a single Node.js process.

## Overview

The repository demonstrates:

- A Vite React frontend with Monaco-based editing
- Yjs + Socket.IO real-time collaborative editing
- Express static file serving
- Dockerized deployment using a multi-stage Docker build
- Basic AWS/Docker learning materials included in the repo

## Project structure

```text
.
├── Backend/
│   ├── package.json
│   ├── package-lock.json
│   └── server.js
├── Frontend/
│   ├── public/
│   ├── src/
│   ├── .gitignore
│   ├── eslint.config.js
│   ├── index.html
│   ├── package.json
│   ├── package-lock.json
│   ├── vite.config.js
│   └── README.md
├── aws-setup.pdf
├── docker.pdf
├── dockerfile
├── .dockerignore
├── .gitignore
├── README.md
└── LICENSE
```

## Tech stack

### Frontend
- React 19
- Vite
- Monaco Editor
- Tailwind CSS
- Yjs + Socket.IO for collaborative editing

### Backend
- Node.js
- Express
- Socket.IO
- Y-Socket.IO

## How it works

The app starts with a basic username screen. Once a user joins, the frontend opens a Monaco editor and connects to the backend through a Socket.IO provider. Shared document state is synchronized using Yjs, allowing multiple users to edit the same document in real time.

The backend exposes:

- static files from `public`
- health endpoint: `GET /health`
- Socket.IO collaboration server on the same Node process

## Local development

### 1. Install dependencies

Frontend:

```bash
cd Frontend
npm install
```

Backend:

```bash
cd Backend
npm install
```

### 2. Run the frontend

```bash
cd Frontend
npm run dev
```

### 3. Run the backend

```bash
cd Backend
npm start
```

The backend serves the app from the `public` folder, which is populated during the Docker build process. In development, the frontend is typically run separately and served through Vite.

## Docker build and run

This repository includes a multi-stage Docker build in `dockerfile`.

### Build the image

```bash
docker build -t docker-aws .
```

### Run the container

```bash
docker run -p 3000:3000 docker-aws
```

Then open:

```text
http://localhost:3000
```

## Health check

The backend includes a health route:

```bash
curl http://localhost:3000/health
```

Expected response:

```json
{
  "message": "ok",
  "success": true
}
```

## Notes

- The project is intended as an educational copy for learning Docker, deployment workflows, and collaborative web app architecture.
- The repository also contains documentation PDFs for Docker and AWS setup.
- The frontend build output is copied into `Backend/public` during the Docker image build.

## Learning resources in this repo

- `docker.pdf` — Docker concepts and setup notes
- `aws-setup.pdf` — AWS-related setup guidance

## License

This project does not currently declare a project-specific license in the repository metadata. Please check the repository contents and original source before commercial reuse.

## Contributing

This is primarily a learning and experimentation repository. If you want to extend it, you can:

- add better Docker Compose support
- improve project documentation
- add authentication or room-based collaboration
- deploy to a cloud provider such as AWS EC2 or ECS

## Summary

`docker-aws` is a small, practical full-stack project for learning how to package a frontend and backend into a deployable Docker image while building a real-time collaborative application.
