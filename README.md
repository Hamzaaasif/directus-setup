# DIRECTUS

## Create a directus extension
Please follow [DOCUMENTATION](https://docs.directus.io/extensions/creating-extensions.html)

## Create following folders 
- data
- extensions
- tmp
- uploads

This will be used by directus and docker. The folder strucutre should look like this

![image](https://github.com/user-attachments/assets/f2b053ef-7d7a-4e64-ab29-ca8303c5ff73)


## Running directus locally and build extension

### Run the docker compose file 
```
docker-compose up -d
```
The database, redis cache and the directus containers running

### Check the running container
```
docker ps
```
copy the database container name

## Running directus locally using the current project

### Access docker terminal and remove the database in which you want to dump

Access docker terminal

```
docker exec -it <CONTAINER NAME> psql -U <DB_USER> -d <DB_DATABASE>
ex: docker exec -it fat-crm-directus-database-1 psql -U directus -d directus
```
Change the database
```
\c <DB NAME>
ex: \c postgres
```

Stop the backend process so it will not create any tables or fuctions
```
SELECT pg_terminate_backend(pg_stat_activity.pid)
FROM pg_stat_activity
WHERE pg_stat_activity.datname = 'directus'
AND pid <> pg_backend_pid()
```

Drop Database and create new database

```
DROP DATABASE <DB NAME>
ex: DROP DATABASE Directus
```

Recreate Database
```
CREATE DATABASE directus
ex: CREATE DATABASE directus
```

## Dump sql file into the newely created database


```
cat <DUMP FILE PATH> | docker exec -i <CONTAINER NAME> pg_restore -U <DB USER> -d <DB DATABASE>
ex: cat sdb_fatmvs_backup.sql | docker exec -i fat-crm-directus-database-1 pg_restore -U directus -d directus
```

The database will run successfully!!

## Hash password for replace

```
$argon2id$v=19$m=65536,t=3,p=4$cb01V0GK9BcVfMtpg1T99w$ds8Y+tzHpoKkGCFLXKgG4bkHUnYfyUxjkRC5KNmXH4o

with PID password : admin
```
