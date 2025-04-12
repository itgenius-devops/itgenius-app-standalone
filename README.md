

---

```markdown
# ITGenius App - Java Spring Boot + MySQL Deployment Practice

This hands-on project walks you through deploying a Java Spring Boot application connected to a MySQL database using two CentOS servers.

---

## Project Overview

In this practice, you will:

- Set up a dedicated MySQL database server
- Configure a Spring Boot application server
- Enable user registration and login functionality
- Learn how to use environment-based configuration to link your application with a database

---

## Infrastructure Setup

### Step 1: Provision Two Servers

- **Server 1**: Database Server (CentOS, minimum 1 GB RAM)
- **Server 2**: Application Server (CentOS)

---

## Database Server Setup (Server 1)

### Install MySQL on CentOS

Follow this guide to install MySQL on your CentOS server:  
[CentOS 8 MySQL Installation Guide](https://itgenius-team-u5ijt9rh.atlassian.net/wiki/spaces/documentat/pages/14417929/CentOS+8)

### Login and Configure MySQL

Follow this guide for MySQL configuration and commands:  
[MySQL Commands Practice](https://itgenius-team-u5ijt9rh.atlassian.net/wiki/spaces/documentat/pages/14319683/Commands+Practice)

### Inside MySQL, run the following:

#### Step 1: Create a New Database

```sql
CREATE DATABASE itgenius_app_database;
```

#### Step 2: Create a New User

```sql
CREATE USER 'itgenius_app_user'@'%' IDENTIFIED BY 'Databaseuserstrongpassword@123';
```

#### Step 3: Grant Privileges

```sql
GRANT ALL PRIVILEGES ON itgenius_app_database.* TO 'itgenius_app_user'@'%';
```

#### Step 4: Flush Privileges

```sql
FLUSH PRIVILEGES;
```

**Make sure to record the following credentials:**

- Database Name: `itgenius_app_database`
- Username: `itgenius_app_user`
- Password: `Databaseuserstrongpassword@123`

---

## Application Server Setup (Server 2)

### Step 1: Install Java 17

```bash
sudo yum install java-17-openjdk-1:17.0.13.0.11-4.el9.x86_64 -y
```

### Step 2: Clone the Application Repository

```bash
git clone https://github.com/itgenius-devops/itgenius-app-standalone.git
```

```bash
cd itgenius-app-standalone
```

### Step 3: Configure Environment Variables

Edit the `.env` file:

```bash
nano .env
```

Update the file as follows:

```env
DB_URL=jdbc:mysql://<your-database-server-public-ip>:3306/itgenius_app_database
DB_USERNAME=itgenius_app_user
DB_PASSWORD=Databaseuserstrongpassword@123
```

Save and exit the file.

---

## Running the Application

### Run in the Foreground

```bash
java -jar itgenius-0.0.1-SNAPSHOT.jar
```

### Run in the Background and Redirect Logs

```bash
nohup java -jar itgenius-0.0.1-SNAPSHOT.jar > app.log 2>&1 &
```

### Check if the Application is Running

```bash
ps -ef | grep java
```

---

## Accessing the Application

Open your browser and navigate to:

```
http://<your-app-server-public-ip>:8085
```

You should see the application running and ready for user registration and login.

---

## Summary

| Component       | Detail                                        |
|-----------------|-----------------------------------------------|
| DB Server       | Hosts MySQL and `itgenius_app_database`       |
| App Server      | Hosts the Spring Boot application             |
| Port            | Application runs on port `8085`               |
| Java Version    | 17                                            |
| Database        | `itgenius_app_database`                       |
| Credentials     | `itgenius_app_user` / `Databaseuserstrongpassword@123` |

---



---
```

**NOTE: IF USING LIGHTSAIL SERVER, MAKE SURE TO ALLOW PORT 8085 ON THE APPLICATION SERVER AND PORT 3306 ON THE MYSQL DATABASE SERVER.**
