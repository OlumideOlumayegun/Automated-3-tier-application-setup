# Automated 3-Tier Application Setup using Vagrant, VirtualBox, and Bash Scripting with Nginx, Apache Tomcat, MySQL, Memcached, and RabbitMQ

Here is a detailed `README.md` for your GitHub repository:

```markdown
# Automated 3-Tier Application Setup using Vagrant, VirtualBox, and Bash Scripting

This project automates the setup of a 3-tier application environment locally using **Vagrant**, **VirtualBox**, and **Bash scripting**. The services involved in the project are:
- **Nginx** (Web Tier)
- **Apache Tomcat** (App Tier)
- **MySQL** (Database Tier)
- **Memcached** (Caching)
- **RabbitMQ** (Message Queue)

The application follows a 3-tier architecture consisting of:
1. **Web Tier**: Nginx as the reverse proxy and load balancer.
2. **App Tier**: Apache Tomcat for serving the application.
3. **Database Tier**: MySQL for data storage, Memcached for caching, and RabbitMQ for messaging.

## Prerequisites

Before running this project, ensure you have the following installed on your machine:
- **Vagrant**: [Download here](https://www.vagrantup.com/)
- **VirtualBox**: [Download here](https://www.virtualbox.org/)
- **Git**: [Download here](https://git-scm.com/)
- **A text editor** (Optional but recommended): VSCode, Sublime Text, etc.

## Project Structure

```bash
vagrant-3tier-setup/
│
├── Vagrantfile                # Main Vagrant configuration file
├── scripts/                   # Directory for provisioning scripts
│   ├── setup_nginx.sh         # Bash script for Nginx setup
│   ├── setup_tomcat.sh        # Bash script for Tomcat setup
│   └── setup_db_services.sh   # Bash script for MySQL, Memcached, and RabbitMQ setup
└── README.md                  # Project documentation (this file)
```

## How to Use

### Step 1: Clone the Repository

Clone this repository to your local machine:

```bash
git clone https://github.com/your-username/vagrant-3tier-setup.git
cd vagrant-3tier-setup
```

### Step 2: Initialize and Start the Vagrant Environment

Run the following command to initialize and start the virtual machines:

```bash
vagrant up
```

This command will:
- Download the base box (`ubuntu/bionic64`).
- Create three virtual machines: **Web**, **App**, and **DB**.
- Automatically provision the VMs with the corresponding Bash scripts for setting up **Nginx**, **Apache Tomcat**, **MySQL**, **Memcached**, and **RabbitMQ**.

### Step 3: Access the Virtual Machines

Once the VMs are up and running, you can access them using SSH:

- **Web Tier (Nginx)**:
  ```bash
  vagrant ssh web
  ```

- **App Tier (Tomcat)**:
  ```bash
  vagrant ssh app
  ```

- **Database Tier (MySQL, Memcached, RabbitMQ)**:
  ```bash
  vagrant ssh db
  ```

### Step 4: Test the Application

- **Nginx** (Web Tier) should be running on port 80 and accessible via the web browser at the VM's IP address.
- **Tomcat** (App Tier) will be running on port `8080` and can be accessed by navigating to `http://<web_vm_ip>:8080`.
- **MySQL**, **Memcached**, and **RabbitMQ** are running on the **DB Tier**. You can test them by accessing their respective ports:
  - MySQL: Port `3306`
  - Memcached: Port `11211`
  - RabbitMQ: Port `5672` (Management UI on port `15672`)

### Step 5: Destroy the Environment (Optional)

After you're done testing, you can destroy the VMs to clean up resources:

```bash
vagrant destroy
```

This will stop and remove the virtual machines created by Vagrant.

## Bash Script Details

### 1. **setup_nginx.sh**
Installs and configures **Nginx** as a reverse proxy and load balancer for the Web tier.

```bash
#!/bin/bash
sudo apt-get update
sudo apt-get install -y nginx
sudo systemctl start nginx
sudo systemctl enable nginx
```

### 2. **setup_tomcat.sh**
Installs **Apache Tomcat**, a servlet container, and starts the Tomcat server.

```bash
#!/bin/bash
sudo apt-get update
sudo apt-get install -y openjdk-11-jdk
wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.58/bin/apache-tomcat-9.0.58.tar.gz
tar xvf apache-tomcat-9.0.58.tar.gz
sudo mv apache-tomcat-9.0.58 /opt/tomcat
sudo /opt/tomcat/bin/startup.sh
```

### 3. **setup_db_services.sh**
Installs **MySQL**, **Memcached**, and **RabbitMQ** on the DB tier and starts the services.

```bash
#!/bin/bash
sudo apt-get update

# Install MySQL
sudo apt-get install -y mysql-server
sudo systemctl start mysql
sudo systemctl enable mysql

# Install Memcached
sudo apt-get install -y memcached
sudo systemctl start memcached
sudo systemctl enable memcached

# Install RabbitMQ
sudo apt-get install -y rabbitmq-server
sudo systemctl start rabbitmq-server
sudo systemctl enable rabbitmq-server
```

## Networking

This setup uses **private networking** for VMs. The Web, App, and DB VMs can communicate with each other over a private network while remaining isolated from the public network. All three VMs are accessible via their private IPs.

You can find the IP addresses of the VMs by running the following command for each VM:
```bash
vagrant ssh web -c "ip addr show"
vagrant ssh app -c "ip addr show"
vagrant ssh db -c "ip addr show"
```

## Conclusion

This project provides an automated way to set up a 3-tier architecture on your local machine using Vagrant, VirtualBox, and Bash scripting. The project can be extended by adding additional configurations, services, and deployment pipelines as needed.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

---

This `README.md` gives clear instructions on how to set up the project, explaining the functionality of the scripts and the project structure, along with specific details for testing and interacting with the environment. Feel free to adjust any parts to suit your specific setup or modifications!
