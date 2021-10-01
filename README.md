# Buidling the image
cd ./docker
docker build -t pgshard .

## Spin up the containers
docker run --name pgshard1 -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d pgshard
docker run --name pgshard2 -e POSTGRES_PASSWORD=postgres -p 5433:5432 -d pgshard
docker run --name pgshard3 -e POSTGRES_PASSWORD=postgres -p 5434:5432 -d pgshard

## Connect to container
docker exec -it pgshard1 psql -U postgres

# Spin up pgadmin
docker run --name pgadmin -p 5555:80 -e 'PGADMIN_DEFAULT_EMAIL=postgres@postgres.com' -e 'PGADMIN_DEFAULT_PASSWORD=postgres' -d dpage/pgadmin4

## Command to inspect which port run docker container
docker inspect pgshard1

## Example requests:
Requests.http

### Generate sequence in Postgres
insert into temp(t) values select random()*100 from generate_series(0, 1000000);
