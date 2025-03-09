# DATABASE-BACKUP-AND-RECOVERY--TASK-4
### **CODTECH INTERNSHIP TASK - 4: DATABASE BACKUP AND RECOVERY**

**Objective:**
This task aims to demonstrate the process of **backing up a database** and **restoring** it in case of a failure. The backup ensures the safety of the data, while the recovery process helps restore the database in case of failure, corruption, or accidental data loss. The deliverables for this task include **SQL scripts** for backup and recovery, along with a **documentation report** detailing the process.

---

### **Process Overview**

The backup and recovery process involves two major steps:
1. **Backup**: Creating a copy of the database and storing it for future use.
2. **Recovery**: Restoring the database from the backup if any failure or data loss occurs.

For this task, we'll demonstrate how to back up and restore a database using both **MySQL** and **PostgreSQL**.

---

### **1. BACKUP AND RECOVERY PROCESS FOR MYSQL**

#### **Backup MySQL Database**

To back up a MySQL database, we use the `mysqldump` command. This command generates a backup of the entire database into a `.sql` file, which can later be restored.

**SQL Command for Backup:**

```bash
mysqldump -u username -p database_name > /path/to/backup/database_name_backup.sql
```

- `-u username`: MySQL username
- `-p`: Prompts for the password
- `database_name`: Name of the database to back up
- `/path/to/backup/database_name_backup.sql`: Path and filename where the backup will be saved

**Example Command:**

```bash
mysqldump -u root -p company_db > /home/user/backups/company_db_backup.sql
```

#### **Restore MySQL Database from Backup**

To restore a database from a backup in MySQL, use the following command:

**SQL Command for Restore:**

```bash
mysql -u username -p database_name < /path/to/backup/database_name_backup.sql
```

- `-u username`: MySQL username
- `-p`: Prompts for the password
- `database_name`: Name of the database to restore
- `/path/to/backup/database_name_backup.sql`: Path to the backup file

**Example Command:**

```bash
mysql -u root -p company_db < /home/user/backups/company_db_backup.sql
```

---

### **2. BACKUP AND RECOVERY PROCESS FOR POSTGRESQL**

#### **Backup PostgreSQL Database**

To back up a PostgreSQL database, we use the `pg_dump` command. This command creates a backup in a custom format (compressed), which is suitable for later restoration.

**SQL Command for Backup:**

```bash
pg_dump -U username -F c -b -v -f /path/to/backup/database_name_backup.dump database_name
```

- `-U username`: PostgreSQL username
- `-F c`: Custom format (compressed)
- `-b`: Include large objects
- `-v`: Verbose mode (for detailed output)
- `-f /path/to/backup/database_name_backup.dump`: Path and filename for the backup
- `database_name`: Name of the database to back up

**Example Command:**

```bash
pg_dump -U postgres -F c -b -v -f /home/user/backups/company_db_pg_backup.dump company_db_pg
```

#### **Restore PostgreSQL Database from Backup**

To restore the backup of a PostgreSQL database, we use the `pg_restore` command.

**SQL Command for Restore:**

```bash
pg_restore -U username -d database_name -v /path/to/backup/database_name_backup.dump
```

- `-U username`: PostgreSQL username
- `-d database_name`: The target database to restore to
- `-v`: Verbose mode (for detailed output)
- `/path/to/backup/database_name_backup.dump`: Path to the backup file

**Example Command:**

```bash
pg_restore -U postgres -d company_db_pg -v /home/user/backups/company_db_pg_backup.dump
```

---

### **3. BACKUP AND RECOVERY SCRIPTS**

#### **MySQL Backup Script (bash)**

```bash
#!/bin/bash
# MySQL Backup Script

DB_NAME="company_db"
USER="root"
BACKUP_DIR="/home/user/backups"
DATE=$(date +%F)

# Create a backup of the MySQL database
mysqldump -u $USER -p $DB_NAME > $BACKUP_DIR/$DB_NAME\_backup_$DATE.sql

echo "Backup completed: $BACKUP_DIR/$DB_NAME\_backup_$DATE.sql"
```

#### **MySQL Restore Script (bash)**

```bash
#!/bin/bash
# MySQL Restore Script

DB_NAME="company_db"
USER="root"
BACKUP_FILE="/home/user/backups/company_db_backup.sql"

# Restore the database from backup
mysql -u $USER -p $DB_NAME < $BACKUP_FILE

echo "Restore completed: $DB_NAME restored from $BACKUP_FILE"
```

#### **PostgreSQL Backup Script (bash)**

```bash
#!/bin/bash
# PostgreSQL Backup Script

DB_NAME="company_db_pg"
USER="postgres"
BACKUP_DIR="/home/user/backups"
DATE=$(date +%F)

# Create a backup of the PostgreSQL database
pg_dump -U $USER -F c -b -v -f $BACKUP_DIR/$DB_NAME\_backup_$DATE.dump $DB_NAME

echo "Backup completed: $BACKUP_DIR/$DB_NAME\_backup_$DATE.dump"
```

#### **PostgreSQL Restore Script (bash)**

```bash
#!/bin/bash
# PostgreSQL Restore Script

DB_NAME="company_db_pg"
USER="postgres"
BACKUP_FILE="/home/user/backups/company_db_pg_backup.dump"

# Restore the database from backup
pg_restore -U $USER -d $DB_NAME -v $BACKUP_FILE

echo "Restore completed: $DB_NAME restored from $BACKUP_FILE"
```

---

### **4. DOCUMENTATION OF THE BACKUP AND RECOVERY PROCESS**

#### **Backup Process**

- **MySQL**: 
  - Use the `mysqldump` command to create a `.sql` backup of the database.
  - The backup file contains both the database schema (structure) and data, making it suitable for a full recovery.
  
- **PostgreSQL**: 
  - Use the `pg_dump` command with a custom format to back up the database. This backup is compressed and efficient.
  - The `.dump` file is suitable for efficient restoration and includes the database schema, data, and large objects.

#### **Recovery Process**

- **MySQL**: 
  - Use the `mysql` command to restore the database from the `.sql` backup file. The database structure and data are fully restored.
  
- **PostgreSQL**: 
  - Use the `pg_restore` command to restore the database from the `.dump` backup file. It restores both the schema and data of the database.

#### **Best Practices for Backup and Recovery**
- **Frequency**: Schedule regular backups, either daily or weekly, depending on your use case.
- **Offsite Storage**: Store backups in an offsite location or use cloud services to ensure safety in case of hardware failure.
- **Automation**: Automate the backup and recovery process using scripts to reduce human error and ensure consistency.
- **Testing**: Periodically test backup and recovery procedures to ensure they work when needed.

---

### **Conclusion**

This task demonstrated how to **back up** and **restore** databases in **MySQL** and **PostgreSQL**. The key steps involved using utility commands (`mysqldump`, `pg_dump`, and `pg_restore`) to back up the database and restore it in case of failure. Additionally, we provided **bash scripts** to automate both the backup and recovery processes. 

