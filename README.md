## 🧩 What is CrsMgr?

**CrsMgr (Course Manager)** is a web-based academic course management system developed at Concordia University. It is designed to assist instructors with managing project-based university courses efficiently. The platform handles everything from group assignments and file submissions to automated grading and peer evaluation.

### ✅ Key Features

- 🏫 Course and session setup
- 👥 Group formation and student enrollment
- 🧑‍🏫 Professor assignment
- 📝 Assignment submissions and file uploads (up to 25MB)
- 🔁 Peer review system with configurable forgiveness logic
- 🧮 Automated grading using Worst-by-Average (WBA) logic
- 📤 Grade export in CSV format
- ⏱️ Quiz buffer time handling based on number of questions
- 🔐 Role-based access (Admin, Professor, Student)
- 📊 Alphabetical sorting of students, including late registrants

---

## 🖥️ What You’ll Need

| Component       | Purpose                                    |
|----------------|--------------------------------------------|
| Apache Server  | To host the CrsMgr website locally         |
| MySQL/MariaDB  | To store student, course, and grade data   |
| PHP            | To run the server-side logic               |
| Web Browser    | To interact with the system                |
| Terminal       | For manual database setup (no `setup.php`) |

---

## 🧰 Step 1: Install Required Software

### 🔹 Windows (using XAMPP)

1. Download **XAMPP** from  
   [https://www.apachefriends.org/index.html](https://www.apachefriends.org/index.html)

2. Install XAMPP and launch the **XAMPP Control Panel**

3. Start these two services:  
   ✅ Apache  
   ✅ MySQL

---

### 🔹 Linux (Ubuntu/Debian)

1. Open a terminal and run:

   ```bash
   sudo apt update
   sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql unzip
   ```

2. Start Apache and MySQL:

   ```bash
   sudo systemctl start apache2
   sudo systemctl start mysql
   ```

3. Optional: Enable them to start on boot:

   ```bash
   sudo systemctl enable apache2
   sudo systemctl enable mysql
   ```

---

## 📁 Step 2: Place the CrsMgr Files

1. Copy or download the `CrsMgr` project folder.

2. Move it into your web server directory:

   - **Windows**:  
     Place it in  
     ```
     C:/xampp/htdocs/crsmgr/
     ```

   - **Linux**:  
     Run:
     ```bash
     sudo cp -r CrsMgr /var/www/html/crsmgr
     sudo chown -R www-data:www-data /var/www/html/crsmgr
     sudo chmod -R 755 /var/www/html/crsmgr
     ```

---

## 🗃️ Step 3: Create and Initialize the Database

### ✅ 1. Create the database

```bash
mysql -u root -p
```

Inside the MySQL prompt:

```sql
CREATE DATABASE crsmgr;
USE crsmgr;
```

### ✅ 2. Import table structure

Exit MySQL prompt and run from terminal:

```bash
mysql -u root -p crsmgr < /path/to/tables-desc.sql
```

> Replace `/path/to/` with the actual path to the `tables-desc.sql` file.

---

## 👤 Step 4: Manually Add an Admin User

Login to MySQL:

```bash
mysql -u root -p
USE crsmgr;
```

Run:

```sql
INSERT INTO USER (USER_ID, USER_NAME, PASSWORD, ACCESS_PRIV)
VALUES (1000, 'admin', 'admin123', 'A');
```

| Field         | Meaning                          |
|---------------|----------------------------------|
| `USER_ID`     | Must be unique (e.g., 1000)      |
| `USER_NAME`   | Username for login               |
| `PASSWORD`    | Password (plaintext)             |
| `ACCESS_PRIV` | `'A'` = Admin, `'P'` = Professor |

---

## 🌐 Step 5: Access the System

Open a web browser and go to:

```
http://localhost/crsmgr/
```

Log in with:

- **Username**: `admin`  
- **Password**: `admin123`

You should now be able to use the full CrsMgr system.

---

## 🔧 Optional: Increase Upload Limit

### Linux (PHP-FPM based):

1. Edit PHP-FPM config:

   ```bash
   sudo nano /etc/php/7.x/fpm/php.ini
   sudo nano /etc/php-fpm.d/www.conf
   ```

   Add or modify:

   ```
   upload_max_filesize = 25M
   post_max_size = 26M
   ```

   In `www.conf`, under `[www]`:

   ```
   php_admin_value[upload_max_filesize] = 25M
   php_admin_value[post_max_size] = 26M
   php_admin_value[upload_tmp_dir] = /tmp/CrsMgr
   ```

2. Restart services:

   ```bash
   sudo systemctl restart php7.x-fpm
   sudo systemctl restart apache2
   ```

---

## 📄 Understand Database Schema

- `tables-desc.sql`: SQL structure to create all necessary tables
- `tables-desc.txt`: Text description of each table and its purpose

View with:

```bash
cat tables-desc.txt
```

---

## 🧪 Testing Checklist

| Task                     | What to Do                               |
|--------------------------|------------------------------------------|
| Login                    | Use `/crsmgr/` → admin/admin123          |
| Add courses and students | Use Admin panel                          |
| Peer review              | Assign groups, submit reviews            |
| Upload test files        | Try uploading PDF/ZIP ≤ 25MB             |
| Export grades            | Click **Create Grade CSV**               |

---

## 🛠️ Troubleshooting

| Problem                 | Likely Cause or Fix                                |
|------------------------|-----------------------------------------------------|
| Page not found         | Check Apache is running and correct path used      |
| Table not found errors | Ensure `tables-desc.sql` was imported correctly     |
| Login doesn’t work     | Check if admin user was inserted into `USER` table |
| File upload fails      | Verify `upload_max_filesize` and `post_max_size`   |

---

## 📞 Help & Contact

For questions or issues, contact:

**Dr. Bipin C. Desai**  
Concordia University  
📧 BipinC.Desai@concordia.ca
