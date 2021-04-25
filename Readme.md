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

---

Find Demo Image at [docker hub](https://hub.docker.com/repository/docker/cliffenator/mssql-docker-compose)

> Note the above image is only for local evaluation. Do not use it in production. For use in production clone this repository.

<div>
      <h6 style="float:center;">Courtesy of <span><a href="https://dbafromthecold.com/2020/07/17/sql-server-and-docker-compose/" target="_blank">DbaFromTheCold</a></span></h6>
<div>
