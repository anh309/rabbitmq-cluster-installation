# RabbitMQ Cluster

1.  Install RabbitMQ
2.  Check status
3.  Add user, vhost, permissions

## 1. Install RabbitMQ
### Start rabbitmq-01

RabbitMQ params is defined in file `.env`

```
RABBITMQ_ERLANG_COOKIE=abcd12345
RABBITMQ_DEFAULT_USER=admin
RABBITMQ_DEFAULT_PASS=Vng@12345678
RABBITMQ_DEFAULT_VHOST=/

```
`docker-compose up -d`

### Start rabbitmq-02, rabbitmq-03

rabbitmq-02, rabbitmq-03 start with entrypoint `cluster-entrypoint.sh`

`docker-compose up -d`

### Install Additional Plugins

Copy plugins to directory `plugins`

Check plugins

`docker exec -it <container name> rabbitmq-plugins list`

Enable plugin 

`docker exec -it rabbit-1 rabbitmq-plugins enable <plugin name>`

E.g. Install plugin rabbitmq_delayed_message_exchange

`docker exec -it rabbit-1 rabbitmq-plugins enable rabbitmq_delayed_message_exchange`


## 2. Check status
### Check Cluster status

`docker exec -it <container name> rabbitmqctl cluster_status`


## 3. Add user, vhost, permissions
### Create user

Add user

`rabbitmqctl add_user udevmyplus QfobY@47NJftJVum8nqUPMeGb`

Set user as administrator

`rabbitmqctl set_user_tags test administrator`

### Permissions
Set permissions on vhost /

`rabbitmqctl set_permissions -p / udevmyplus ".*" ".*" ".*"`


### Add virtual host

`rabbitmqctl add_vhost 123cs`
