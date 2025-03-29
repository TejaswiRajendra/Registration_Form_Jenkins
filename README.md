# **Registration Form Deployment using Jenkins and GitHub**  

# **Project Overview**
This project automates the deployment of a Registration Form (Frontend Only) using Jenkins and GitHub. The form is hosted on an AWS EC2 instance and updated automatically through a Jenkins CI/CD pipeline whenever changes are pushed to GitHub.

# Project Requirements
1. Infrastructure Requirements
AWS EC2 Instance (Ubuntu/Amazon Linux for hosting)

Security Groups (Allow HTTP (port 80) or HTTPS (port 443))

Elastic IP (Optional, for a fixed public IP)

2. Software Requirements
GitHub (Stores the frontend code)

Jenkins (Automates deployment)

Web Server (Apache/Nginx) (Hosts the static frontend)

HTML, CSS, JavaScript (Frontend code)

3. Jenkins Plugins
Git Plugin (To fetch code from GitHub)

Pipeline Plugin (For automated deployment)

SSH Pipeline Steps (To connect to the EC2 instance)
Deployment Procedure
1. Setup GitHub Repository
Create a GitHub repository and push the registration form files (index.html, style.css, script.js).
2. Configure the EC2 Web Server
Launch an EC2 instance (Ubuntu/Amazon Linux).

Install Apache/Nginx to serve static files.
3. Configure Jenkins for Deployment
Install Jenkins on a server or use an existing Jenkins instance.

Install required plugins (Git, SSH Pipeline, Pipeline).

Create a Jenkins Pipeline Job to pull the latest code and copy it to the EC2 instance.

4. Write a Jenkinsfile for Automation
The Jenkinsfile will:

Pull the latest code from GitHub.

SSH into the EC2 instance.

Copy the frontend files to the web server directory.

Restart the web server.
5. Deploy the Application
Push changes to GitHub, and Jenkins will automatically deploy them to EC2.

Access the registration form using the EC2 public IP.
