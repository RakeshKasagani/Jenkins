# Installing Jenkins on Ubuntu, Creating Your First Job, and Managing Users

🧩 Part 1: Install Jenkins on Ubuntu

Step 1: Update and upgrade system

sudo apt update -y

sudo apt upgrade -y

Step 2: Install Java (Jenkins requires Java 11 or 17)

Jenkins needs Java (OpenJDK).


sudo apt install fontconfig openjdk-21-jre


Verify:

java -version


Expected output:

openjdk 21.0.8 2025-07-15
OpenJDK Runtime Environment (build 21.0.8+9-Debian-1)
OpenJDK 64-Bit Server VM (build 21.0.8+9-Debian-1, mixed mode, sharing)

Step 3: Add Jenkins repository and key

Jenkins is not in the default Ubuntu repo, so we add it manually.

sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key


Now add the repository:

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

Step 4: Install Jenkins
sudo apt update
sudo apt install jenkins -y

Step 5: Start and enable Jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins


Check status:

sudo systemctl status jenkins


You should see:
Active: active (running)

Step 6: Adjust Firewall (if UFW is enabled)

By default Jenkins runs on port 8080.

Allow Jenkins through the firewall:

sudo ufw allow 8080
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status

Step 7: Access Jenkins Web UI

Open a browser and go to:

http://<your-server-public-ip>:8080


Example:

http://54.234.208.154:8080

Step 8: Unlock Jenkins

Get the initial admin password:

sudo cat /var/lib/jenkins/secrets/initialAdminPassword


Copy the key and paste it into the Jenkins web page → “Unlock Jenkins”.

Step 9: Install suggested plugins

Choose “Install suggested plugins”

Wait for plugins to install (it may take a few minutes)

Step 10: Create your first Admin User

After plugin installation, Jenkins asks for an admin user:

Username: admin

Password: yourpassword

Full name: Administrator

Email: your@email.com

Then click “Save and Continue”

Step 11: Jenkins setup complete

You’ll see:
✅ “Jenkins is ready!”

Click “Start using Jenkins”.

🧱 Part 2: Create Your First Jenkins Job (Pipeline or Freestyle)
Option 1: Create a Freestyle Job (Basic)

From Jenkins Dashboard → Click “New Item”

Enter an item name: e.g. MyFirstJob

Select Freestyle project

Click OK

In “Description” field → write something like:
This is my first Jenkins job

Under Build, click Add build step → Execute shell

Add a command:

echo "Hello, Jenkins is running successfully!"
date


Click Save

Click Build Now

👉 After it runs, click Build #1 → Console Output to see:

Hello, Jenkins is running successfully!
Mon Oct 27 17:00:00 IST 2025


✅ Your first job is done!

You’ll see the pipeline run in stages visually.

👥 Part 3: Create New Users in Jenkins

Step 2: Add users manually

From Dashboard → Click Manage Jenkins → Users

Click Create User

Fill details:

Username: developer1

Password: password123

Full name: Developer 1

Email: dev1@example.com

Click Create User

Step 3: Assign roles (optional, if using Matrix Authorization)

If you want to control permissions:

Go to Manage Jenkins → Configure Global Security

Scroll to Authorization → Matrix-based security

Add the username you created

Check appropriate permissions (e.g. build, read, configure)

Click Save

