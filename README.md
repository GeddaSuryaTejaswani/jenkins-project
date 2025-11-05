# Jenkins CI/CD with Git, Docker, and Email Notifications

This project demonstrates an automated Jenkins pipeline that:
- Pulls code from GitHub using the Git plugin
- Builds and runs a Docker container with the Docker plugin
- Sends build notifications using the Email Extension plugin

## Steps to Use

1. Install Jenkins and required plugins:
   - Git Plugin
   - Docker Plugin
   - Email Extension Plugin

2. Configure SMTP in Jenkins (Manage Jenkins → System → Extended E-mail Notification).

3. Connect Jenkins to Docker:
   - Ensure Docker is installed and Jenkins has permission to run it.

4. Create a Pipeline job in Jenkins pointing to this GitHub repo.

5. Build the pipeline and view results!
