
# 📘 CrsMgr System – Installation Guide (Windows)

## 🔧 Introduction

**CrsMgr** (Course Manager System) is a web-based platform developed at Concordia University to manage project-based courses with features like assignment submissions, peer evaluation, WBA (Worst-by-Average) grading, automated grade calculation, CSV export, and more. This README provides step-by-step instructions to install and configure CrsMgr on a Windows machine using **XAMPP**.

---

## 🖥️ System Requirements

- Windows 10/11
- XAMPP (includes Apache, MySQL, PHP)
- Web Browser (Chrome/Firefox recommended)

---

## 📥 Step 1: Install Apache, MySQL, and PHP (XAMPP)

1. **Download XAMPP**:
   - Visit: [https://www.apachefriends.org/en/xampp-windows.html](https://www.apachefriends.org/en/xampp-windows.html)
   - Choose the **latest version** and download the **EXE (7-ZIP)** Self-extracting archive.

2. **Extract XAMPP**:
   - Extract the package to `C:/xampp` or the root of another partition (recommended for path simplicity).

3. **Start Servers**:
   - Run `xampp-control.exe` from the `C:/xampp` directory.
   - Start **Apache** and **MySQL**.
   - Confirm by visiting: [http://localhost](http://localhost)

---

## 📁 Step 2: Install CrsMgr System

1. **Download CrsMgr**:
   - Use the demo or full version from:
     [https://crsmgr.encs.concordia.ca/crsmgr](https://crsmgr.encs.concordia.ca/crsmgr)

2. **Extract to XAMPP Directory**:
   - Extract the contents into:
     ```
     C:/xampp/htdocs/crsmgr/
     ```

3. **Database Setup**:
   - Open your browser and navigate to:
     ```
     http://localhost/crsmgr/setup.php
     ```
   - Follow the instructions to:
     - Create the database (default name: `crsmgr`)
     - Configure tables
     - Set up admin account

4. **Final Installation Step**:
   - Access the system at:
     ```
     http://localhost/crsmgr/
     ```
   - Log in using the created credentials.

---

## ✅ Features & Enhancements (as per latest update)

- ✅ Upload files up to **25MB** (PHP-FPM configuration updated)
- ✅ **WBA (Worst-by-Average)** logic configurable for 1, 2, or 3 lowest marks
- ✅ **CSV export**: Clean file with Student ID, Last Name, First Name, Letter Grade
- ✅ Alphabetical sorting of students including late registrants
- ✅ Accurate **peer review attribution** to reviewees (not reviewers)
- ✅ **Peer forgiveness logic**: One missing peer review can be averaged
- ✅ Enhanced **quiz time buffer logic** (based on quiz time & number of questions)
- ✅ Improved exception handling and user experience

---

## 🛠️ Configuration Notes (PHP File Upload Limits)

Ensure the following is correctly set (especially if using PHP-FPM):

### Edit `/etc/php-fpm.d/www.conf`:
```
php_admin_value[upload_max_filesize] = 25M
php_admin_value[post_max_size] = 26M
php_admin_value[upload_tmp_dir] = /tmp/CrsMgr
```

---

## 📤 Exporting Grades

You can download the grades CSV:
- Click **"Create Grade CSV"** on the UI
- Now supports **sorting by Last Name or Student ID**

---

## 🧪 Testing Tips

Use:
- Upload sample files (individual/group) up to 25MB
- Test peer review visibility
- Check CSV output format
- Validate WBA updates and grade reflection

---

## 🔒 Notes

- Ensure `htdocs/crsmgr` folder has appropriate read/write permissions.
- MySQL user must have privileges to create and alter the `crsmgr` database.

---

## 📞 Support

For issues, contact the course administrator or your system supervisor (e.g., Dr. Bipin Desai at Concordia University).
