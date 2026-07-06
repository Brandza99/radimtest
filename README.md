# GitHub Actions Docker CI/CD Refresh

This project demonstrates a simple CI/CD workflow using GitHub Actions, Docker, Docker Hub, and Docker Compose.

## Flow

1. Code is changed locally.
2. Changes are pushed to GitHub.
3. GitHub Actions starts automatically on push.
4. The workflow checks out the repository code.
5. Docker builds an image from the Dockerfile.
6. GitHub Actions logs in to Docker Hub using GitHub Secrets.
7. The image is pushed to Docker Hub with version and latest tags.
8. A separate deploy folder pulls the image from Docker Hub.
9. Docker Compose runs the application using the selected image tag from `.env`.

## Technologies

- Git
- GitHub
- GitHub Actions
- Docker
- Docker Hub
- Docker Compose
- Nginx

## Important Notes

- Docker Hub credentials are stored as GitHub Secrets.
- The Docker Hub token is not written in the workflow file.
- The deploy server does not build the image.
- The deploy server only pulls and runs an existing image from Docker Hub.
- `.env` is ignored by Git.
- `.env.example` is committed as a safe template.

## Commands Used For Deploy

```bash
docker compose config
docker compose pull
docker compose up -d
curl localhost:8360

Rollback
Rollback is done by changing IMAGE_TAG in .env to an older stable version and running:

docker compose pull
docker compose up -d

Summary
When code is pushed to GitHub, GitHub Actions builds a Docker image and pushes it to Docker Hub.
 The deploy folder then pulls the selected image tag and runs it with Docker Compose.

```bash
git add README.md
git commit -m "Add project README"
git push
