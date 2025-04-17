

---

# **ITGenius App Deployment Guide**  
**Technology Stack: Java Spring Boot + MySQL**  
*Environment: Two CentOS Servers*

This hands-on project provides a practical walkthrough for deploying a Java Spring Boot application connected to a MySQL database using two separate CentOS-based servers.

---

## 🔍 **Project Overview**

In this exercise, you will:

- Provision a dedicated MySQL database server
- Set up a Spring Boot application server
- Implement user registration and login functionality
- Utilize environment-based configurations to connect your application to the database

---

## 🛠️ **Infrastructure Setup**

### Step 1: Provision Two CentOS Servers

- **Server 1**: MySQL Database Server  
  - OS: CentOS  
  - Minimum: 1 GB RAM  
- **Server 2**: Application Server  
  - OS: CentOS  

---

## 🗄️ **Database Server Configuration (Server 1)**

### 1. Install MySQL

Follow this guide to install MySQL on your CentOS database server:  
🔗 [CentOS 8 MySQL Installation Guide](https://itgenius-team-u5ijt9rh.atlassian.net/wiki/spaces/documentat/pages/14417929/CentOS+8)

### 2. Log in and Configure MySQL

Refer to the following guide for MySQL commands and best practices:  
🔗 [MySQL Command Guide](https://itgenius-team-u5ijt9rh.atlassian.net/wiki/spaces/documentat/pages/14319683/Commands+Practice)

Once inside the MySQL shell, execute the following:

#### a. Create a New Database

```sql
CREATE DATABASE itgenius_app_database;
```

#### b. Create a Database User

```sql
CREATE USER 'itgenius_app_user'@'%' IDENTIFIED BY 'Databaseuserstrongpassword@123';
```

#### c. Grant User Privileges

```sql
GRANT ALL PRIVILEGES ON itgenius_app_database.* TO 'itgenius_app_user'@'%';
```

> Optional: For limited privileges, use:

```sql
GRANT CREATE, ALTER, DROP, SELECT, INSERT, UPDATE, DELETE ON itgenius_app_database.* TO 'itgenius_app_user'@'%';
```

#### d. Flush Privileges

```sql
FLUSH PRIVILEGES;
```

📌 **Credentials to Note:**

- **Database Name**: `itgenius_app_database`
- **Username**: `itgenius_app_user`
- **Password**: `Databaseuserstrongpassword@123`

---

## 🚀 **Application Server Configuration (Server 2)**

### Step 1: Install Java 17

```bash
sudo yum install java-17-openjdk-1:17.0.13.0.11-4.el9.x86_64 -y
```

### Step 2: Install MySQL Client (Not Server)

MySQL Client allows the app server to communicate with the MySQL database remotely.

#### a. Add the MySQL Yum Repository

```bash
sudo yum install https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm -y
```

#### b. Install MySQL Client

```bash
sudo yum install mysql -y
```

### Step 3: Clone the Application Repository

```bash
git clone https://github.com/itgenius-devops/itgenius-app-standalone.git
cd itgenius-app-standalone
```

### Step 4: Configure Environment Variables

Open the `.env` file for editing:

```bash
vi .env
```

Update the following variables with your database server details:

```
DB_URL=jdbc:mysql://<your-database-server-public-ip>:3306/itgenius_app_database
DB_USERNAME=itgenius_app_user
DB_PASSWORD=Databaseuserstrongpassword@123
```

Save and close the file.

---

> ⚠️ **Important**:  
If you are using Amazon Lightsail, go into the lightsail console in AWS and under the "Networking" tab, make sure to  :
- Open **port 8085** on the **Application Server** (for web access)
- Open **port 3306** on the **Database Server** (for MySQL connectivity)

---

## ▶️ **Running the Application**

### Run in Foreground

```bash
java -jar itgenius-0.0.1-SNAPSHOT.jar
```

### Run in Background with Logs

```bash
nohup java -jar itgenius-0.0.1-SNAPSHOT.jar >> /var/log/app.log 2>&1 &
```

### Verify Application is Running

```bash
ps -ef | grep java
```

---

## 🌐 **Accessing the Application**

Open your browser and visit:

```
http://<your-app-server-public-ip>:8085
```

You should see the application interface, allowing user registration and login.

---

## 📋 **Summary Table**

| Component        | Description                                      |
|------------------|--------------------------------------------------|
| **Database Server** | Hosts MySQL and `itgenius_app_database`         |
| **Application Server** | Hosts the Java Spring Boot Application        |
| **App Port**      | `8085`                                           |
| **Java Version**  | Java 17                                          |
| **Database Name** | `itgenius_app_database`                          |
| **Username**      | `itgenius_app_user`                              |
| **Password**      | `Databaseuserstrongpassword@123`                |

---

Thank You
