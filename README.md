# postgres
#start docker
docker run --name CONTAINER_NAME --restart=always -e POSTGRES_PASSWORD=1 -d -p 5432:5432 -v VOLUME_NAME:/var/lib/postgresql/data -v /mnt/backup:/backup ledangtuanbk/postgres:9.6

#Create database:
CREATE DATABASE "DB_NAME" WITH OWNER "postgres" ENCODING 'UTF8' LC_COLLATE = 'en_US.UTF-8' LC_CTYPE = 'en_US.UTF-8' TEMPLATE template0;

#Backup database:
docker exec -t $CONTAINER_NAME pg_dump -U postgres --no-owner -Fc $DB_NAME -f /backup/${DB_NAME}dump$(date +%Y%m%d"_"%H%M%S).dmp

#restore database :
docker exec -t CONTAINER_NAME pg_restore -U postgres -d DB_NAME -1 /backup/backup_file.dmp
