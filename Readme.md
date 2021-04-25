# Microsoft Sql Server Linux Container
<small>With segregated persistence volumes and environment variable files to ease.</small>
<hr>

### Requirements:
- Docker with docker-compose

# How to run:

## Method 1 - By Cloning

1. Clone https://github.com/infinity-arc/infinity-arc-portal.git
2. cd mssql-docker-compose
3. Update the password in the `sapassword.env` file save and close.
4. run `docker-compose up -d`  
5. Connect to `localhost` username: `sa` password: `<the password from the sapassword.env>`
 
## Method 2 - Create the files

#### 1. Create a file named docker compose and place the following content in it.

```yaml
version: '3.8'
services:
  identity-database:
    build:
      context: .
      dockerfile: dockerfile
    ports:
      - "1433:1433"
    env_file:
      - MSSQL_SA_PASSWORD=<sql-server-admin-password>
      - ACCEPT_EULA=Y
      - MSSQL_DATA_DIR=/var/opt/sqlserver/data
      - MSSQL_LOG_DIR=/var/opt/sqlserver/log
      - MSSQL_BACKUP_DIR=/var/opt/sqlserver/backup
    volumes:
      - sqlsystem:/var/opt/mssql/
      - sqldata:${MSSQL_DATA_DIR}
      - sqllog:${MSSQL_LOG_DIR}
      - sqlbackup:${MSSQL_BACKUP_DIR}
volumes:
  sqlsystem:
  sqldata:
  sqllog:
  sqlbackup:
```
#### 2. In the same directory create a `dockerfile` with the content below

```dockerfile
# build from the Ubuntu 18.04 image
FROM ubuntu:20.10
 
# create the mssql user
RUN useradd -u 10001 mssql
 
# installing SQL Server
RUN apt-get update && apt-get install -y wget software-properties-common apt-transport-https
RUN wget -qO- https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
RUN apt-get update && apt-get install -y mssql-server
 
# creating directories
RUN mkdir /var/opt/sqlserver
RUN mkdir /var/opt/sqlserver/data
RUN mkdir /var/opt/sqlserver/log
RUN mkdir /var/opt/sqlserver/backup
 
# set permissions on directories
RUN chown -R mssql:mssql /var/opt/sqlserver
RUN chown -R mssql:mssql /var/opt/mssql
 
# switching to the mssql user
USER mssql
 
# starting SQL Server
CMD /opt/mssql/bin/sqlservr
```
> NOTE Ensure that the directories in the `docker-compose.yml` and `dockerfile` always remain the same if you wish to do your own configuration.

#### 3. Run `docker-compose up -d`

## Method 3 - Pull the files using curl

```bash
curl https://raw.githubusercontent.com/infinity-arc/mssql-docker-compose/master/docker-compose.yml -o docker-compose.yml
curl https://raw.githubusercontent.com/infinity-arc/mssql-docker-compose/master/dockerfile -o ddockerfile
curl https://raw.githubusercontent.com/infinity-arc/mssql-docker-compose/master/sapassword.env -o sapassword.env
curl https://raw.githubusercontent.com/infinity-arc/mssql-docker-compose/master/sqlserver.env -o sqlserver.env
```
#### Run `docker-compose up -d`

---
##### Courtesy of [DbaFromTheCold](https://dbafromthecold.com/2020/07/17/sql-server-and-docker-compose/)
