What does your user need to know to try your project?

## Prerequisites
MOF depends on one of bellow database needs to be installed.

| Database   | Suggested Version |
|------------|-------------------|
| MySQL      | >5.6              |
| PostgreSQL | >8.4              |
| SQL Server | >8.4              |
| SQLite     | >15.0             |

- Run MySQL from docker

```bash
docker run --name mysql -e MYSQL_ROOT_PASSWORD=my-password -d mysql:tag
```

## Install
MOF can be installed as bellow.

- Docker
- Kubernetes
- From source

### Docker
Create docker-compose.yaml as bellow.

- docker-compose.yaml

```yaml
version: '3'
services:
  dash:
    image: pointgoal/dash:latest
    ports:
      - 80:80
  mof:
    image: pointgoal/mof-backend:latest
    ports:
      - 8080:8080
    environment:
      # Override your mysql address
      - RK_MYSQL_0_ADDR=host.docker.internal:3306
      # Override your mysql username and password
      - RK_MYSQL_0_USER=root
      - RK_MYSQL_0_PASS=my-pass
```

- Run docker-compose

```bash
docker-compose -f docker-compose.yaml up
```

### Kubernetes
```bash
$ todo
```

### From source

```bash
$ todo
```