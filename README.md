# Automated Multi-Tier Application Setup using Vagrant, VirtualBox, and Bash Scripting with Nginx, Apache Tomcat, MySQL, Memcached, and RabbitMQ

This project automates the setup of a multi-tier application environment locally using **Vagrant**, **VirtualBox**, and **Bash scripting** for the deployment of a Java application social networking app.  

The services involved in the project are:
- **Nginx** (Web Tier): as the reverse proxy and load balancer
- **Apache Tomcat** (App Tier): for serving the Java application
- **MySQL** (Database Tier): for data storage
- **Memcached** (Caching)
- **RabbitMQ** (Message Queue)

## Prerequisites

Before running this project, ensure you have the following installed on your machine:
- **Vagrant**: [Download here](https://www.vagrantup.com/)
- **VirtualBox**: [Download here](https://www.virtualbox.org/)
- **Git**: [Download here](https://git-scm.com/)
- **A text editor** (Optional but recommended): e.g. VSCode

## Project Structure

```bash
automated_setup/
│
├── Vagrantfile                # Main Vagrant configuration file
└── scripts/                   # Directory for provisioning scripts
    ├── setup_nginx.sh         # Bash script for Nginx setup
    ├── setup_tomcat.sh        # Bash script for Tomcat setup
    ├── setup_mysql.sh         # Bash script for MySQL setup
    ├── setup_memcache.sh      # Bash script for Memcached setup
    └── setup_rabbitmq         # Bash script for RabbitMQ setup
```

## How to Use

### Step 1: Clone the Repository

Clone this repository to your local machine:

```bash
git clone https://github.com/OlumideOlumayegun/Automated-3-tier-application-setup.git
cd Automated-3-tier-application-setup/automated_setup
```

### Step 2: Initialise and Start the Vagrant Environment

Run the following command to initialise and start the virtual machines:

```bash
vagrant up
```

This command will:
- Download the base box.
- Create five virtual machines: **web01**, **app01**, **db01**, **mc01**, and **rmq01**.
- Automatically provision the VMs with the corresponding Bash scripts for setting up **Nginx**, **Apache Tomcat**, **MySQL**, **Memcached**, and **RabbitMQ**.

### Step 3: Access the Virtual Machines

Once the VMs are up and running, you can access them using SSH:

- **Web Tier (Nginx)**:
  ```bash
  vagrant ssh web01
  ```

- **App Tier (Tomcat)**:
  ```bash
  vagrant ssh app01
  ```

 - **Database Tier (MySQL)**:
  ```bash
  vagrant ssh db01
  ```
- **Memcached**:
  ```bash
  vagrant ssh mc01
  ```

- **RabbitMQ**:
  ```bash
  vagrant ssh rmq01
  ```

### Step 4: Test the Application

- **Nginx** (Web Tier) should be running on port 80 and accessible via the web browser at the VM's IP address.
- **Tomcat** (App Tier) will be running on port `8080` and can be accessed by navigating to `http://<web_vm_ip>:8080`.

### Step 5: Destroy the Environment (Optional)

After you're done testing, you can destroy the VMs to clean up resources:

```bash
vagrant destroy
```

This will stop and remove the virtual machines created by Vagrant.

## Networking

This setup uses **private networking** for VMs. The VMs can communicate with each other over a private network while remaining isolated from the public network. All five VMs are accessible via their private IPs.

You can find the IP addresses of the VMs by running the following command for each VM:
```bash
vagrant ssh web01 -c "ip addr show"
vagrant ssh app01 -c "ip addr show"
vagrant ssh db01 -c "ip addr show"
vagrant ssh mc01 -c "ip addr show"
vagrant ssh rmq01 -c "ip addr show"
```

## Conclusion

This project provides an automated way to set up a multi-tier architecture on your local machine using Vagrant, VirtualBox, and Bash scripting. The project can be extended by adding additional configurations, services, and deployment pipelines as needed.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

This `README.md` gives clear instructions on how to set up the project, explaining the functionality of the scripts and the project structure, along with specific details for testing and interacting with the environment. Feel free to adjust any parts to suit your specific setup or modifications!
