Here’s a clean and professional `README.md` file for your Spring Boot + MySQL practice project:

---

```markdown
# 🧠 ITGenius App - Java Spring Boot + MySQL Deployment Practice

This hands-on project is designed to teach students how to connect a Java Spring Boot application to a MySQL database using a real-world deployment scenario involving two CentOS servers.

---

## 🚀 Project Overview

In this exercise, you'll:
- Set up a dedicated **MySQL database server**
- Configure a **Spring Boot application server**
- Enable **user registration and login**
- Learn how environment variables and database credentials integrate into application configurations

---

## 🧱 Infrastructure Setup

### 🖥️ 1. Provision Two Servers

- **Server 1**: Database Server (CentOS, minimum 1 GB RAM)
- **Server 2**: Application Server (CentOS)

---

## 🛠️ Database Server Setup (Server 1)

### 🔹 Install MySQL on CentOS
Follow this guide to install MySQL:
👉 [CentOS 8 MySQL Installation Guide](https://itgenius-team-u5ijt9rh.atlassian.net/wiki/spaces/documentat/pages/14417929/CentOS+8)

### 🔹 Configure MySQL
Then use this guide to access MySQL and execute commands:
👉 [MySQL Command Lines](https://itgenius-team-u5ijt9rh.atlassian.net/wiki/spaces/documentat/pages/14319683/Commands+Practice)

### 🔹 Inside MySQL, run the following:

```sql
-- Step 1: Create a new database
CREATE DATABASE itgenius_app_database;

-- Step 2: Create a new user
CREATE USER 'itgenius_app_user'@'%' IDENTIFIED BY 'Databaseuserstrongpassword@123';

-- Step 3: Grant privileges
GRANT ALL PRIVILEGES ON itgenius_app_database.* TO 'itgenius_app_user'@'%';
FLUSH PRIVILEGES;
```

📝 **Record These Credentials:**
- **Database Name**: `itgenius_app_database`
- **Username**: `itgenius_app_user`
- **Password**: `Databaseuserstrongpassword@123`

---

## 🧩 Application Server Setup (Server 2)

### 🔹 Step 1: Install Java 17
```bash
sudo yum install java-17-openjdk-1:17.0.13.0.11-4.el9.x86_64 -y
```

### 🔹 Step 2: Clone the App Repository
```bash
git clone https://github.com/itgenius-devops/itgenius-app-standalone.git
cd itgenius-app-standalone
```

### 🔹 Step 3: Configure Environment Variables

Edit the `.env` file and update the following fields:

```env
DB_URL=jdbc:mysql://<your-database-server-public-ip>:3306/itgenius_app_database
DB_USERNAME=itgenius_app_user
DB_PASSWORD=Databaseuserstrongpassword@123
```

Save and exit.

---

## 🚦 Running the Application

### ✅ Foreground Mode
```bash
java -jar itgenius-0.0.1-SNAPSHOT.jar
```

### ✅ Background Mode (with logs redirected)
```bash
nohup java -jar itgenius-0.0.1-SNAPSHOT.jar > app.log 2>&1 &
```

Check running processes:
```bash
ps -ef | grep java
```

---

## 🌐 Accessing the Application

Open your browser and navigate to:

```
http://<your-app-server-public-ip>:8085
```

You should see the application running and ready for user registration/login.

---

## 📚 Summary

| Component | Detail |
|----------|--------|
| **DB Server** | Hosts MySQL & database |
| **App Server** | Hosts Spring Boot app |
| **Port** | App runs on port `8085` |
| **Java Version** | 17 |
| **Database** | `itgenius_app_database` |
| **Credentials** | `itgenius_app_user` / `Databaseuserstrongpassword@123` |

---

Happy learning! 🎓  
Feel free to explore, break things, and ask questions!

```
**NOTE: IF USING LIGHTSAIL SERVER, MAKE SURE TO ALLOW PORT 8085 ON THE APPLICATION SERVER AND PORT 3306 ON THE MYSQL DATABASE SERVER.**
