# **Deploying  Todo List on EC2 using PHP**

[](https://github.com/Afaq-Devxops/Pny-Batch_3_4/blob/EC2/AWS%20EC2%20lab%203%20Todo%20List%20with%20PHP.md#deploy-the-todo-list-with-php-on-ec2)

### **Step 1: Launch an Ubuntu EC2 Instance**

[](https://github.com/Afaq-Devxops/Pny-Batch_3_4/blob/EC2/AWS%20EC2%20lab%203%20Todo%20List%20with%20PHP.md#step-1-launch-an-ubuntu-ec2-instance)

1. **Log in to the AWS Console** and navigate to the EC2 Dashboard.
    
2. **Launch an Instance:**
    
    - **AMI:** Select **Ubuntu Server 24.04 LTS**.
    - **Instance Type:** `t2.micro` (Free Tier Eligible).
    - **Key Pair:** Create or use an existing key pair.
    - **Security Group:**
        - Allow **HTTP (Port 80)** from 0.0.0.0/0.
        - Allow **SSH (Port 22)** from your IP.
3. **Launch the Instance.**
    

---

### **Step 2: Connect to the EC2 Instance**

[](https://github.com/Afaq-Devxops/Pny-Batch_3_4/blob/EC2/AWS%20EC2%20lab%203%20Todo%20List%20with%20PHP.md#step-2-connect-to-the-ec2-instance)

1. **SSH into the instance:**
    
    ```shell
    ssh -i "your-key-file.pem" ubuntu@<INSTANCE_PUBLIC_IP>
    ```
    
2. **Update the system:**
    
    ```shell
    sudo apt update -y
    sudo apt upgrade -y
    ```
    

---

### **Step 3: Install Apache, PHP, and MySQL**

[](https://github.com/Afaq-Devxops/Pny-Batch_3_4/blob/EC2/AWS%20EC2%20lab%203%20Todo%20List%20with%20PHP.md#step-3-install-apache-php-and-mysql)

1. **Install Apache:**
    
    ```shell
    sudo apt install apache2 -y
    ```
    
2. **Install PHP and Required Modules:**
    
    ```shell
    sudo apt install php libapache2-mod-php php-mysql -y
    ```
    
3. **Install MySQL:**
    
    ```shell
    sudo apt install mysql-server -y
    ```
    
4. **Secure MySQL Installation:**
    
    ```shell
    sudo mysql_secure_installation
    ```
    
    - Set a root password and follow the prompts to secure MySQL.

---

### **Step 4: Set Up the Database**

[](https://github.com/Afaq-Devxops/Pny-Batch_3_4/blob/EC2/AWS%20EC2%20lab%203%20Todo%20List%20with%20PHP.md#step-4-set-up-the-database)

1. **Log into MySQL:**
    
    ```shell
    sudo mysql -u root -p
    ```
    
2. **Create a Database:**
    
    ```sql
    CREATE DATABASE todo;
    EXIT;
    ```
    
3. **Import the `todo.sql` File:**
    
    - Clone the GitHub repository:
        
        ```shell
        sudo apt install git -y
        git clone https://github.com/ali-azgar-rakib/Todo-list-with-php.git
        ```
        
    - Navigate to the repository directory:
        
        ```shell
        cd Todo-list-with-php
        ```
        
    - Import the `todo.sql` file into the `todo` database:
        
        ```shell
        sudo mysql -u root -p todo < todo.sql
        ```
        

---

### **Step 5: Deploy the Application**

[](https://github.com/Afaq-Devxops/Pny-Batch_3_4/blob/EC2/AWS%20EC2%20lab%203%20Todo%20List%20with%20PHP.md#step-5-deploy-the-application)

1. **Move the Application Files:**
    
    - Move all files from the cloned repository to the Apache web directory:
        
        ```shell
        sudo mv * /var/www/html/
        ```
        
2. **Set Permissions:**
    
    - Ensure Apache has access to the files:
        
        ```shell
        sudo chmod -R 755 /var/www/html/
        ```
        
3. **Restart Apache:**
    
    ```shell
    sudo systemctl restart apache2
    ```
    

---

### **Step 6: Test the Application**

[](https://github.com/Afaq-Devxops/Pny-Batch_3_4/blob/EC2/AWS%20EC2%20lab%203%20Todo%20List%20with%20PHP.md#step-6-test-the-application)

1. Open your browser and navigate to:
    
    ```
    http://<INSTANCE_PUBLIC_IP>
    ```
    
2. **What You Should See:**
    
    - A working To-Do List application with options to:
        - Add tasks.
        - View tasks.
        - Edit tasks.
        - Delete tasks.

---

### **Step 7: Secure and Clean Up**

[](https://github.com/Afaq-Devxops/Pny-Batch_3_4/blob/EC2/AWS%20EC2%20lab%203%20Todo%20List%20with%20PHP.md#step-7-secure-and-clean-up)

1. **Restrict SSH Access:**
    
    - Update your EC2 Security Group to allow SSH only from your IP address.
2. **Stop or Terminate the Instance (if not needed).**



---



### **Conclusion**

You’ve successfully deployed a PHP-based To-Do List application on an EC2 instance! You can now manage tasks, edit to-do items, and access the application from anywhere using the public IP (or your custom domain if configured).




---
---
