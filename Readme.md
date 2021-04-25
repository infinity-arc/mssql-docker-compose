# Microsoft Sql Server Linux Container
<small>with segregated persistence</small>

### Requirements:
- Docker with docker-compose

### How to run:
1. Clone this repo
2. cd mssql-docker-compose
3. Update the password in the `sapassword.env` file save and close.
4. run `docker-compose up -d`  
5. Connect to `localhost` username: `sa` password: `<the password from the sapassword.env>`

Courtesy of [dbafromthecold](https://dbafromthecold.com/2020/07/17/sql-server-and-docker-compose/) 
