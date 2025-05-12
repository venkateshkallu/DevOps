## Learning Docker: Accessing PostgreSQL, Exporting & Importing Data

 In this phase of our Docker journey, we explored how to work with **PostgreSQL inside containers**. 

 The guide is written with **early learners** in mind — especially those starting with containerization and databases.

---

 #### Step 1: Install Docker

 ```bash
 sudo apt update
 sudo apt install docker.io
 sudo systemctl start docker
 sudo systemctl enable docker
 ```


 #### Step 2: Run a PostgreSQL Container
  Now let’s start a PostgreSQL container with persistent storage using Docker volumes.

 ```bash
 docker run --name pg-container \
 -e POSTGRES_USER=admin \
 -e POSTGRES_PASSWORD=secret \
 -e POSTGRES_DB=mydb \
 -v pgdata:/var/lib/postgresql/data \
 -p 5432:5432 \
 -d postgres:latest
 ```


 #### Step 3: Access the PostgreSQL Shell
 Use the following command to access the running Postgres container:

 ```bash

 docker exec -it pg-container psql -U admin -d mydb

```
Once inside, you’re at the psql prompt and can begin interacting with the database.


#### Step 4: Run Basic CRUD Operations
Try running these SQL commands inside the container:
```sql
-- Create a table
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name TEXT,
  email TEXT
);

-- Insert data
INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
INSERT INTO users (name, email) VALUES ('Bob', 'bob@example.com');

-- Read data
SELECT * FROM users;

-- Update data
UPDATE users SET name = 'Alice Smith' WHERE id = 1;

-- Delete data
DELETE FROM users WHERE id = 2;

-- Verify
SELECT * FROM users;
```
These operations help verify that the container is functional and your database is accessible.



#### Step 5: Persist Data on Restart (Using Docker Volumes)
Container data is lost on removal by default. Use Docker volumes to persist PostgreSQL data.

1. Create a directory on your host machine

```

mkdir -p ~/postgres_data

```
This folder will store your database files

2. Run PostgreSQL with a volume:

```bash
docker run --name pg-container \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=secret \
  -e POSTGRES_DB=mydb \
  -v pgdata:/var/lib/postgresql/data \
  -p 5432:5432 \
  -d postgres:latest
```
This ensures that PostgreSQL writes data to a persistent volume on your host.

3. Restart and check persistence:

```bash

docker restart pg-container

```
4. Access the shell again and run a query:

```bash

docker exec -it pg-container psql -U admin -d mydb

```
5. After restart, check data:

```sql
SELECT * FROM users;
To recreate the container without losing data:

```bash

docker rename pg-container pg-container-old

```
Now you can reuse the name and volume with a new container.


#### Step 6: Export Data from the Container to Local Machine
You can create a folder on your local machine to store all your backups neatly:

```bash

mkdir -p ~/postgres_backups
cd ~/postgres_backups

```

Export PostgreSQL Database to a Local .sql Backup File
```bash

docker exec -t pg-container pg_dump -U admin mydb > mydb_backup.sql
```
After this command, the backup file will be saved in your current directory on Ubuntu.


#### Step 7: Import Data into Another PostgreSQL Container
1. Run a New PostgreSQL Container
```bash
docker run --name pg-container-import \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=secret \
  -e POSTGRES_DB=mydb \
  -d postgres:latest
```
Wait a few seconds for it to fully start.

2. Copy Backup File into the New Container
Assuming your backup file is in ~/postgres_backups:

```bash

docker cp ~/postgres_backups/mydb_backup.sql pg-container-import:/mydb_backup.sql
```
3. Import the Data
Run this to restore the data:

```bash

docker exec -it pg-container-import \
  psql -U admin -d mydb -f /mydb_backup.sql
```
4. Verify the Data
Access the new container:

```bash

docker exec -it pg-container-import psql -U admin -d mydb
```

Then run:

```sql
SELECT * FROM users;
```
--------------------------------------------------------------------------------------------------------------------
Follow these seven steps to master PostgreSQL management in Docker on Ubuntu, from setup to backup and restoration.
Happy learning and keep building!
