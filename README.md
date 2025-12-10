# Assignment: OpenShift Guestbook with GitHub Actions Automation

## Contributors
- Rani Perwitasari  
- Serhat Bilge  


---

## Project Overview
This project is based on the Guestbook application and demonstrates deployment of a cloud-native, multi-container application on OpenShift using GitHub Actions. Key features include:

- Two containers: **Frontend** and **Backend**  
- Persistent storage using **PostgreSQL**  
- Caching using **Redis**  
- Configuration management using **ConfigMaps** and **Secrets**  
- Automated build, publish, and deployment with **GitHub Actions**  
- External routing using OpenShift **Route**

---

## Solution Approach

### 1. GitHub Actions Workflow
The workflow is triggered automatically on a `git push` to the repository. The steps include:

1. Build **Backend container**  
2. Build **Frontend container**  
3. Publish both containers to **GHCR**  
   - Currently using **public images**  
   - In the future, images will be **private**, using authentication and `imagePullSecrets` in the YAML files  
4. Deploy the updated images to **OpenShift**  
   - After publishing, the deployment YAML files are updated to reference the new images  
   - Deployments use the updated image tags to run the latest version of the application

### 2. OpenShift Deployment
- **Deployments updated** to use the new image tags from GHCR  
- **ConfigMaps and Secrets** created for environment variables and credentials  
- **Persistent volumes** configured for PostgreSQL data  
- **Frontend exposed** externally via Route  

<img width="1421" height="486" alt="Screenshot 2025-12-10 at 13 53 42" src="https://github.com/user-attachments/assets/40b7c8d5-efde-4faa-a895-f65810dbcb66" />

<img width="1349" height="1018" alt="Screenshot 2025-12-10 at 13 53 20" src="https://github.com/user-attachments/assets/fdc05bde-b427-44e7-9b6a-5c32c05104d7" />



