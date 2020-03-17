# MongoDB Local ReplicaSet

Sometimes you need a replica set in your local environment (perhaps you want to use the oplog). But it's somewhat involved to spin up a series of mongo containers and provide the correct configuration. This docker image will create a self-contained 3 node replica set (that is, all three nodes are running in one container).

**THIS IS ONLY USEFUL FOR LOCAL DEVELOPMENT**

## Using

You need to know the following:

#### PORTS
Each instance exposes a port, all listening on 0.0.0.0 interface:

  - db1: `27017` [primary]
  - db2: `27018`
  - db3: `27019`

#### DATA
The container will create one volume at `/data`, but you can mount one or more to your host at these paths:

  - db1: `/data/db1` [primary]
  - db2: `/data/db2`
  - db3: `/data/db3`

#### REPLICA SET NAME
You can customize the replica set name by providing `REPLICA_SET_NAME` environment variable. default name is: `rs0`

## Notes

If you mount something into `/data/db1`, the container will not go through it's initialization process, but it will also assume that you have mounted all 3 volumes -- so mount all 3 or none. You can customize the username/password by providing `USERNAME`/`PASSWORD` environment variables (but you probably don't need to).

### Example Run

    docker run -d -p 27017:27017 -p 27018:27018 -p 27019:27019 --name mongo-rs -v mongo-rs-data:/data -e "REPLICA_SET_NAME=mongo-rs" --restart=always flqw/docker-mongo-local-replicaset

### Example Mongo Connection String (from another container)

    mongodb://dev:dev@mongo:27017,mongo:27018,mongo:27019/db
