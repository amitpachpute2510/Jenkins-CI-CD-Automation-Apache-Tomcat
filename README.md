# 🚀 Jenkins CI/CD Automation – Apache & Tomcat

Automating web application deployment on **Ubuntu Linux using Jenkins, Git, GitHub, Apache HTTP Server, and Apache Tomcat**.

## 📌 Project Overview

This project demonstrates how to automate web application deployment using Jenkins and GitHub. It includes deployment workflows for static HTML content hosted on Apache HTTP Server and a web application deployed on Apache Tomcat.

The objective is to reduce manual deployment tasks, maintain backup copies, apply controlled file permissions, and verify deployments after execution.

## 🎯 Project Objectives

- Automate deployment using Jenkins.
- Integrate GitHub with Jenkins for source code management.
- Deploy static web content to Apache HTTP Server.
- Deploy web application files to Apache Tomcat.
- Maintain timestamped backups before deployment.
- Use Bash scripts to automate deployment tasks.
- Verify deployed applications using `curl`.
- Document the setup, configuration, and troubleshooting process.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Jenkins | CI/CD automation |
| Git & GitHub | Version control and source code management |
| Ubuntu Linux | Deployment environment |
| Bash Shell Scripting | Deployment automation |
| Apache HTTP Server | Hosting static web content |
| Apache Tomcat | Hosting Java web applications |
| HTML | Sample web application content |
| Linux Permissions & Sudo | Controlled deployment access |
| curl | Deployment verification |

## 📄 Project Documentation

1. 📘 [Jenkins CI/CD Pipeline – GitHub Integration, Automated Build, Deployment & Testing on Linux Server (PDF)](https://github.com/amitpachpute2510/Jenkins-CI-CD-Automation-Apache-Tomcat/blob/main/Jenkins%20CI_CD%20Pipeline_%20GitHub%20Integration%2C%20Automated%20Build%2C%20Deployment%20%26%20Testing%20on%20Linux%20Server.pdf)

2. 📗 [Jenkins CI/CD Pipeline – Tomcat & Apache: GitHub Integration, Automated Build, Deployment & Testing on Linux Server (PDF)](https://github.com/amitpachpute2510/Jenkins-CI-CD-Automation-Apache-Tomcat/blob/main/Jenkins%20CI_CD%20Pipeline%20%20Tomcat-Apache%20_%20GitHub%20Integration%2C%20Automated%20Build%2C%20Deployment%20%26%20Testing%20on%20Linux%20Server.pdf)

## 🏗️ Project Architecture

```text
             Developer
                 |
                 v
          Update HTML / Code
                 |
                 v
              GitHub
                 |
                 v
              Jenkins
                 |
          Checkout Source
                 |
                 v
        Validate Deployment Files
                 |
                 v
       Create Timestamped Backup
                 |
          +------+------+
          |             |
          v             v
   Apache HTTP       Apache Tomcat
   Server            Server
          |             |
          v             v
   Static Website    Web Application
          |             |
          +------+------+
                 |
                 v
       Verify Deployment using curl
```

## ✨ Key Features

### 1. GitHub Integration
- Store project files in a GitHub repository.
- Track changes through Git commits.
- Allow Jenkins to retrieve the latest committed version.

### 2. Jenkins Automation
- Execute deployment jobs from the Jenkins dashboard.
- Run configured pipeline stages and shell scripts.
- Support automated build triggering through SCM polling when configured.

### 3. Apache HTTP Server Deployment
- Deploy static HTML files to the Apache document root.
- Keep the website files organized in a dedicated directory.
- Verify the deployed website using HTTP requests.

### 4. Tomcat Deployment
- Deploy the sample HTML application to the Tomcat web application directory.
- Automate file validation, backup creation, and deployment.
- Verify the deployed application using HTTPS where required by the Tomcat connector.

### 5. Backup Management
- Create timestamped backups of deployment files.
- Preserve existing deployed content before replacing it.
- Keep build backups and deployment backups in separate directories.

### 6. Permission Management
- Apply controlled ownership and file permissions.
- Restrict privileged deployment operations through an explicitly authorized deployment script.
- Avoid granting Jenkins unrestricted root access.

## 📂 Repository Structure

```text
jenkins-tomcat-demo/
├── README.md
├── Jenkinsfile
├── index.html
├── scripts/
│   └── deploy-jenkins-demo
├── docs/
│   ├── setup-guide.md
│   └── screenshots/
│       ├── jenkins-success.png
│       ├── github-repository.png
│       ├── tomcat-application.png
│       └── deployment-backups.png
└── .gitignore
```

*Note: Add the files and screenshots that actually exist in your repository. If Apache and Tomcat use separate Jenkins jobs, scripts, or repositories, document each workflow separately.*

## ⚙️ Deployment Environment

Example environment used for this project:

| Component | Configuration |
|---|---|
| Operating System | Ubuntu Linux |
| Jenkins Workspace | `/var/lib/jenkins/workspace/jenkins-tomcat-demo` |
| Tomcat Installation | `/opt/apache-tomcat-10.1.56` |
| Tomcat Application | `/opt/apache-tomcat-10.1.56/webapps/jenkins-demo/` |
| Build Backups | `/opt/deploy/tomcat-html/build_backup/` |
| Deployment Backups | `/opt/deploy/tomcat-html/deployment_backup/` |
| Apache Document Root | `/var/www/html/` |

These paths are examples from the configured environment and may need to be changed for another server.

## 🔄 CI/CD Workflow

1. Update the project files.
2. Commit and push changes to GitHub.
3. Jenkins retrieves the latest source code.
4. Jenkins executes the configured pipeline.
5. The deployment script validates the required files.
6. A timestamped backup is created.
7. The updated files are deployed to the target server directory.
8. File ownership and permissions are applied as configured.
9. The application is checked using `curl`.
10. Jenkins reports the job result in its console output.

## 🚀 Getting Started

### Prerequisites

Install and configure the following components:

- Ubuntu Linux
- Git
- Jenkins
- Apache HTTP Server
- Apache Tomcat
- Bash
- A GitHub repository
- Appropriate Jenkins credentials and deployment permissions

### Step 1: Clone the Repository

```bash
git clone https://github.com/amitpachpute2510/jenkins-tomcat-demo.git

cd jenkins-tomcat-demo
```

### Step 2: Configure Jenkins

1. Open the Jenkins dashboard.
2. Create a Pipeline job.
3. Select **Pipeline script from SCM**.
4. Select **Git** as the source control system.
5. Enter the repository URL.
6. Configure the branch as `*/main`.
7. Set the script path to `Jenkinsfile`.
8. Save the job and run a build.

### Step 3: Configure Deployment Permissions

Configure the deployment script, required directory permissions, and narrowly scoped `sudo` access according to the server environment.

Do not grant Jenkins unrestricted root privileges for deployment.

### Step 4: Configure Automated Triggering

To check GitHub for changes periodically, enable **Poll SCM** in the Jenkins job and use this schedule:

```text
H/2 * * * *
```

This checks for source control changes approximately every two minutes. A build is triggered when Jenkins detects relevant changes. This is polling, not an instant GitHub webhook.

### Step 5: Verify Deployment

For the Tomcat demo:

```bash
curl -k -s https://127.0.0.1:8686/jenkins-demo/ | grep -i '<title>'
```

For the Apache demo, if it is deployed at `/jenkins-demo/`:

```bash
curl -I http://127.0.0.1/jenkins-demo/
```

Use `-k` only for local testing with a self-signed TLS certificate. For production, validate certificates properly.

## 💾 Backup Locations

The Tomcat demo uses these directories:

```text
/opt/deploy/tomcat-html/
├── build_backup/
└── deployment_backup/
```

Timestamped folders help distinguish deployment versions and locate previous copies when troubleshooting.

**Important:** A backup is useful only if it contains the files required for recovery. Test the restore procedure before relying on backups in a production environment.

## 📸 Project Screenshots

Add your actual screenshots to `docs/screenshots/` and display them here.

### Jenkins Pipeline

![Jenkins Pipeline Success](https://raw.githubusercontent.com/amitpachpute2510/Jenkins-CI-CD-Automation-Apache-Tomcat/refs/heads/main/Jenkin%20Home.png)

### GitHub Repository

![GitHub Repository](https://raw.githubusercontent.com/amitpachpute2510/Jenkins-CI-CD-Automation-Apache-Tomcat/refs/heads/main/GitHub%20Repository.png)  

### Deployment Backup

![Deployment Backup](https://raw.githubusercontent.com/amitpachpute2510/Jenkins-CI-CD-Automation-Apache-Tomcat/refs/heads/main/Deployment%20Backup.png)

### Tomcat Application

![Tomcat Application](https://raw.githubusercontent.com/amitpachpute2510/Jenkins-CI-CD-Automation-Apache-Tomcat/refs/heads/main/Tomcat%20Application.png)

## 🧰 Troubleshooting

| Problem | What to check |
|---|---|
| Jenkins build fails | Review the Jenkins Console Output |
| GitHub checkout fails | Verify the repository URL, branch, and credentials |
| Permission denied | Check file ownership, permissions, and deployment authorization |
| Application returns 404 | Verify the deployment directory and URL context path |
| HTTPS connection fails | Check the Tomcat HTTPS connector and certificate configuration |
| Changes are not deployed | Confirm the commit was pushed and the Jenkins job checked out the latest revision |
| Automatic deployment does not trigger | Review the SCM polling configuration and Jenkins logs |

## 🔐 Security Best Practices

- Never commit passwords, API tokens, private keys, or sensitive configuration files.
- Use Jenkins credentials instead of hardcoding secrets.
- Grant Jenkins only the permissions required for deployment.
- Keep deployment scripts executable only by authorized users.
- Review backup access permissions.
- Use valid TLS certificates for production services.
- Keep GitHub repositories free of confidential application data.

## 📈 Skills Demonstrated

- CI/CD pipeline configuration
- Git and GitHub version control
- Jenkins job and pipeline management
- Linux administration
- Bash scripting
- Apache and Tomcat deployment
- File permissions and access control
- Backup and recovery planning
- HTTP/HTTPS troubleshooting
- Application deployment verification

## 👨‍💻 Author

**Amit Pachpute**

GitHub: [amitpachpute2510](https://github.com/amitpachpute2510)

---
