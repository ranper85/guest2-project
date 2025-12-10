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
The workflow is triggered automatically on a `git push` to the `main` branch. It has three jobs: **frontend**, **backend**, and **deployment**.

**Frontend Job:**
1. Checkout repository  
2. Build frontend Docker image: `docker build -t frontend:${{ github.sha }} ./frontend`  
3. Tag images for GHCR:
   - `ghcr.io/ranper85/guest2-frontend:${{ github.sha }}`
   - `ghcr.io/ranper85/guest2-frontend:latest`
4. Login to GHCR using `DOCKER_TOKEN` secret  
5. Push both tags to GHCR  

**Backend Job:**
1. Checkout repository  
2. Build backend Docker image: `docker build -t backend:${{ github.sha }} ./backend`  
3. Tag images for GHCR:
   - `ghcr.io/ranper85/guest2-backend:${{ github.sha }}`
   - `ghcr.io/ranper85/guest2-backend:latest`
4. Login to GHCR using `DOCKER_TOKEN` secret  
5. Push both tags to GHCR  

<img width="1421" height="486" alt="Screenshot 2025-12-10 at 13 53 42" src="https://github.com/user-attachments/assets/40b7c8d5-efde-4faa-a895-f65810dbcb66" />

**Deployment Job:**
1. Checkout repository  
2. Login to OpenShift using `OCP_TOKEN` secret:  
   `oc login --token=${{ secrets.OCP_TOKEN }} --insecure-skip-tls-verify --server=https://api.devops24.cloud2.se:6443`  
3. Switch to project: `oc project grupp1`  
4. Apply all YAML files for deployment, services, config, and PVCs:
   - Frontend & Backend deployments  
   - PostgreSQL & Redis deployments  
   - Persistent volume claims for PostgreSQL & Redis  
   - ConfigMaps for backend  
   - Services for frontend, backend, PostgreSQL, Redis  
   - Route for frontend  

**Future improvements:**  
- Make GHCR container images private and configure OpenShift authentication to pull the containers, currently using public GHCR images.
- Only apply YAML files that were changed.  
- Restart deployments when ConfigMaps or Secrets are updated. 

---


### 2. OpenShift Deployment
- **Deployments updated** to use the new image tags from GHCR  
- **ConfigMaps and Secrets** created for environment variables and credentials  
- **Persistent volumes** configured for PostgreSQL data  
- **Frontend exposed** externally via Route  



<img width="1349" height="1018" alt="Screenshot 2025-12-10 at 13 53 20" src="https://github.com/user-attachments/assets/fdc05bde-b427-44e7-9b6a-5c32c05104d7" />



