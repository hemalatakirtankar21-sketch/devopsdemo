# DevOps Demo - Maven WAR Application

A small JSP web application for practicing GitHub -> Maven -> Tomcat deployment.

## Requirements
- Java 21
- Apache Maven 3.9+
- Apache Tomcat 10.1
- Git

## Build locally or on EC2
```bash
java -version
mvn -version
mvn clean package
ls -lh target/devops-demo.war
```

The build output is `target/devops-demo.war`.

## Push this project to GitHub
Create an empty GitHub repository named `devops-demo`, then run these commands from this project directory:

```bash
git init
git add .
git commit -m "Initial Maven web application"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/devops-demo.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username.

## Clone and build on Amazon Linux 2023
```bash
sudo dnf install -y git
git clone https://github.com/YOUR_USERNAME/devops-demo.git
cd devops-demo
mvn clean package
```

## Deploy to Tomcat 10.1
Assuming Tomcat is installed at `/opt/tomcat` and its service is named `tomcat`:

```bash
sudo cp target/devops-demo.war /opt/tomcat/webapps/
sudo systemctl restart tomcat
```

If you run Tomcat manually instead of as a systemd service, use its startup script:
```bash
sudo /opt/tomcat/bin/startup.sh
```

Open:
`http://YOUR_EC2_PUBLIC_IP:8080/devops-demo/`

Allow inbound TCP port 8080 in the EC2 security group only as appropriate for your lab. For a real environment, restrict access and use a reverse proxy/HTTPS.

## Notes
- This project uses JSP and the Jakarta EE 10 web descriptor, suitable for Tomcat 10.1.
- Tomcat 10.1 requires Java 11 or later; Java 21 is suitable.
- Do not run `systemctl restart tomcat` unless you have configured a systemd service with that name.
