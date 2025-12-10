# Assignment: OpenShift Guestbook with GitHub Actions Automation

## Contributors
- Rani Perwitasari
- Serhat Bilge 


## Project Overview
This project uses the Guestbook application as a base and demonstrates deployment of a cloud-native, multi-container application on OpenShift using GitHub Action. The project includes:

- Two containers: Frontend and Backend
- Persistent storage (PostgreSQL)
- Caching (Redis)
- Configuration management with ConfigMaps and Secrets
- Automated deployment using GitHub Actions

-------

## How the Task Was Solved

### GitHub Actions
- A push to the repository triggers the workflow.
- Workflow steps:
  1. Build Backend container  
  2. Build Frontend container  
  3. Publish both containers to GHCR
     - Currently using public images  
     - In the future, images will be private, using authentication and `imagePullSecrets' in the YAML files  
  4. Deploy the new versions to OpenShift  

### OpenShift Deployment
- Backend and frontend deployments were updated to use the new image tags.
- ConfigMaps and Secrets were created for environment variables and credentials.
- Persistent volumes were used for PostgreSQL data.
- Route created to expose frontend externally.
  
<img width="1270" height="888" alt="Screenshot 2025-12-10 at 13 41 04" src="https://github.com/user-attachments/assets/27c561f0-1252-4643-94b2-33a878b750cb" />




