# 🌐 3-Tier Application Deployment on AWS EC2 (Manual Setup)

This project demonstrates the manual deployment of a production-ready **3-Tier Architecture** on a single **AWS EC2 (Ubuntu 22.04 LTS)** instance. It covers everything from Database configuration to Nginx Reverse Proxy setup.

---

## 🏗️ Architecture Breakdown
1. **Frontend Layer:** React.js application served as static files by Nginx.
2. **Backend Layer:** Node.js API managed by **PM2** for process persistence.
3. **Database Layer:** MongoDB (NoSQL) installed locally on the EC2 instance.
4. **Web Server & Proxy:** **Nginx** acting as a Web Server for the frontend and a **Reverse Proxy** for the backend API.



---

## 🚀 Step-by-Step Implementation

### Phase 1: Database & Backend Setup
- **System Update:** Initialized the environment using `sudo apt update && sudo apt upgrade -y`.
- **Database:** Installed **MongoDB** using a custom Bash script. Verified service using `systemctl status mongod`.
- **Backend Environment:** - Installed Node.js using **NVM** (Node Version Manager).
  - Cloned the repository and installed dependencies via `npm install`.
- **Process Management:** Deployed the backend using **PM2**.
  - `pm2 start server.js --name backend`
  - `pm2 save` & `pm2 startup` (To ensure the API starts automatically after a server reboot).

### Phase 2: Frontend & Nginx Proxy Configuration
- **Frontend Build:** Configured the `.env` file to point the React app to the Backend API and generated a production build using `npm run build`.
- **Nginx Deployment:**
  - Moved the build files to `/var/www/html`.
  - Configured the Nginx server block to handle routing.
- **Reverse Proxy:** Set up a location block in Nginx (`/api`) to forward requests to the Node.js process running on port 5000/3000.

---

## 🛠️ Skills Demonstrated
- **Linux Administration:** Package management, service handling (systemd), and user permissions.
- **Process Management:** Using **PM2** for monitoring logs and ensuring 100% uptime.
- **Web Networking:** Configuring **Nginx** as a Reverse Proxy to solve CORS issues and secure the backend.
- **Cloud Infrastructure:** Managing AWS Security Groups (Port 80, 22, 443).

---

## 🔍 Verification Commands
- Check Services: `systemctl status nginx` & `pm2 list`
- Monitor Logs: `pm2 logs` & `tail -f /var/log/nginx/error.log`
- API Health: `curl http://localhost:5000/api/health`

---
**Developed by:** [Mazid Hossain](https://www.linkedin.com/in/md-mazid-hossain-293561227/)
