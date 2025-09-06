# Day 1 of My DevOps & DevSecOps Learning Journey

# Learning Docker Using MySQL

   In this guide, we will learn Docker by running and managing MySQL databases. You will gain hands-on experience with data persistence, and backup/restore workflows on Ubuntu.

---

1. **Docker Installation and Introduction**

   * **What is Docker?**
    Docker packages applications and all their dependencies into containers—“ready-to-run” boxes—that ensure your app behaves identically in development, testing, and production.

   * **Install Docker on Ubuntu**

     ```bash
     sudo apt-get update
     sudo apt-get install -y docker.io
     sudo systemctl start docker
     sudo systemctl enable docker
     docker --version
     ```

2. **Run MySQL Container**

   Launch a MySQL container using the official image:

   ```bash
   docker run --name mysql-container \
     -e MYSQL_ROOT_PASSWORD=my-secret-pw \
     -d mysql:latest
   ```

   * `--name mysql-container`: names the container.
   * `-e MYSQL_ROOT_PASSWORD`: sets the root password.
   * `-d`: runs in detached mode.

3. **Access the MySQL Client with exec**

   Use `docker exec` to open the MySQL shell inside the container:

   ```bash
   docker exec -it mysql-container mysql -u root -p
   ```

   Enter the password you set (`my-secret-pw`).

4. **Run Basic CRUD Operations**

   Inside the MySQL shell, execute SQL commands:

   ```sql
   -- Create a database
   CREATE DATABASE mydb;
   USE mydb;

   -- Create a table
   CREATE TABLE notes (
     id INT AUTO_INCREMENT PRIMARY KEY,
     content TEXT NOT NULL
   );

   -- Insert data
   INSERT INTO notes (content) VALUES ('First note');

   -- Read data
   SELECT * FROM notes;

   -- Update data
   UPDATE notes SET content = 'Updated note' WHERE id = 1;

   -- Delete data
   DELETE FROM notes WHERE id = 1;
   ```

5. **Persist Data on Restart**

   By default, container data is lost on removal. To persist MySQL data:

   1. Create a directory on Ubuntu:

      ```bash
      mkdir -p ~/mysql_data
      ```
   2. Run MySQL with volume mount:

      ```bash
      docker run --name mysql-container \
        -e MYSQL_ROOT_PASSWORD=my-secret-pw \
        -v ~/mysql_data:/var/lib/mysql \
        -d mysql:latest
      ```
   3. To reuse or replace existing containers with the same name:

      * **Remove** an old container:

        ```bash
        docker rm mysql-container
        ```
      * **Rename** an existing container:

        ```bash
        docker rename mysql-container mysql-container-old
        ```

6. **Export Data from Container to Local**

   Back up your database to a `.sql` file on Ubuntu:

   1. Create a backup folder:

      ```bash
      mkdir -p ~/mysql_backups
      ```
   2. Run `mysqldump` via `docker exec`:

      ```bash
      docker exec mysql-container \
        sh -c 'exec mysqldump -u root -p"$MYSQL_ROOT_PASSWORD" mydb' \
        > ~/mysql_backups/mydb_backup.sql
      ```

7. **Import Data into Another MySQL Container**

   Restore the backup in a new container:

   1. Launch a new MySQL container:

      ```bash
      docker run --name mysql-container-import \
        -e MYSQL_ROOT_PASSWORD=my-secret-pw \
        -d mysql:latest
      ```
   2. Copy the backup file:

      ```bash
      docker cp ~/mysql_backups/mydb_backup.sql mysql-container-import:/mydb_backup.sql
      ```
   3. Import inside MySQL shell:

      ```bash
      docker exec -it mysql-container-import mysql -u root -p
      ```

      ```sql
      CREATE DATABASE mydb;
      USE mydb;
      SOURCE /mydb_backup.sql;
      ```
   4. Verify:

      ```sql
      SHOW TABLES;
      SELECT * FROM notes;
      ```

---

Follow these seven steps to confidently manage MySQL in Docker on Ubuntu, from installation to backup and restore. Happy learning!
